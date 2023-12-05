```

                        with ras_data as
                 (with a as
                           (SELECT unnest(string_to_array(
                                   'SOH/032714/23-24_ref,SOH/032714/23-24_sub_ref,8905600696283_product_,2_qty', ',')) AS parts)
        -- select a.parts from a where a.parts like '%_ref%' limit 1
                  select (select unnest(string_to_array(a.parts,
                                                        '_ref')) AS reference_no
                          from a
                          where a.parts like '%_ref%'
                          limit 1),
                         (select unnest(string_to_array(a.parts,
                                                        '_sub_ref')) AS sub_reference_no
                          from a
                          where a.parts like '%_sub_ref%'
                          limit 1)
                          ,
                         (select unnest(string_to_array(a.parts,
                                                        '_product_')) AS product_code
                          from a
                          where a.parts like '%_product_%'
                          limit 1),
                         (select unnest(string_to_array(a.parts,
                                                        '_qty')) AS qty
                          from a
                          where a.parts like '%_qty%'
                          limit 1))


                        update stock_transfer_items
                        set product_code=(select ras_data.product_code from ras_data)
                        , update_dt = now()
                        where stock_transfer_items_id =
                              (select stock_transfer_items_id
                               from stock_transfer_items sti
                                        join ras_data on ras_data.reference_no = sti.reference_no
                                   and ras_data.sub_reference_no = sti.sub_reference_no and sti.product_code != ras_data.product_code
                                   and sti.integration_qty = ras_data.qty::int
                               order by stock_transfer_id desc
                               limit 1)


```
