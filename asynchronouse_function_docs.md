Certainly! Here are the code examples explained in Markdown format:

Example 1
python
Copy code
```python
import asyncio

async def main():
    print("A")
    await asyncio.sleep(1)
    print("B")

asyncio.run(main())
This code demonstrates asynchronous programming. The main function prints "A," then awaits a one-second sleep using await asyncio.sleep(1), and finally prints "B." Asynchronous programming allows other tasks to run concurrently. In this case, "A" is printed, followed by a one-second pause, and then "B" is printed.

Example 2
python
Copy code
import asyncio

async def main():
    print("A")
    await other_function()
    print("B")

async def other_function():
    print("1")
    await asyncio.sleep(2)
    print("2")

asyncio.run(main())
In this example, main prints "A," awaits the execution of other_function(), and then prints "B." other_function() prints "1," sleeps for two seconds, and prints "2." The use of await ensures that main waits for other_function() to complete before proceeding. Therefore, the result is "A 1 2 B."

Example 3
python
Copy code
import asyncio

async def main():
    task = asyncio.create_task(other_function())
    print("A")
    print("B")

async def other_function():
    print("1")
    await asyncio.sleep(2)
    print("2")

asyncio.run(main())
In this example, main creates a task using asyncio.create_task(other_function()), prints "A," and then prints "B." The task executes other_function(), which prints "1," sleeps for two seconds, and prints "2." Since main does not await the task, the result is "A B 1," indicating that the task continues running asynchronously after "B" is printed.

Example 4
python
Copy code
import asyncio

async def main():
    task = asyncio.create_task(other_function())
    print("A")
    await asyncio.sleep(1)
    print("B")

async def other_function():
    print("1")
    await asyncio.sleep(2)
    print("2")

asyncio.run(main())
In this example, main creates a task, prints "A," awaits a one-second sleep using await asyncio.sleep(1), and then prints "B." The task runs other_function(), which prints "1," sleeps for two seconds, and prints "2." The await asyncio.sleep(1) introduces a one-second pause before "B" is printed. As a result, the output is "A 1 B."

Example 5
python
Copy code
import asyncio

async def main():
    task = asyncio.create_task(other_function())
    print("A")
    await asyncio.sleep(1)
    print("B")
    await task

async def other_function():
    print("1")
    await asyncio.sleep(2)
    print("2")

asyncio.run(main())
In this example, main creates a task, prints "A," awaits a one-second sleep, prints "B," and then awaits the completion of task. task runs other_function(), which prints "1," sleeps for two seconds, and prints "2." The use of await task ensures that main waits for other_function() to complete before proceeding. Therefore, the result is "A 1 B 2."

Example 6
python
Copy code
import asyncio

async def main():
    task = asyncio.create_task(other_function())
    await task
    print("A")
    await asyncio.sleep(1)
    print("B")

async def other_function():
    print("1")
    await asyncio.sleep(2)
    print("2")

asyncio.run(main())
In this example, main creates a task, awaits the completion of task, prints "A," sleeps for one second using await asyncio.sleep(1), and finally prints "B." other_function() prints "1," sleeps for two seconds, and prints "2." The result is "1 2 A B" because await task ensures that main waits for other_function() to complete before printing "A" and "B."

Example 7
python
Copy code
import asyncio

async def main():
    task = asyncio.create_task(other_function())
    print("A")
    await asyncio.sleep(1)
    print("B")
    return_value = await task
    print(f"R {return_value}")

async def other_function():
    print("1")
    await asyncio.sleep(2)
    print("2")
    return 10

asyncio.run(main())
In this example, main creates a task, prints "A," awaits a one-second sleep, prints "B," and then awaits the completion of task. other_function() prints "1," sleeps for two seconds, prints "2," and returns the value 10. await task ensures that main waits for other_function() to complete before proceeding. The result is "A 1 B 2 R 10," where "R 10" indicates the return value from other_function().





















Async functions: diffrent functions run in concurr

1. there are two cmds pritn a and print b and in between await sleep(1)
- sleep for one second in between


2 . there are two functions main and other_functions 
- condition:
 	await other_function():

	async def main():
		print(“A”)
		await  other_functions():
		print(“”B”)
	async def other_function():
		print(“1”)
		await asyncio.sleep(2)
		print(“2”)
asyncio.run(main())

result A 1 2 B

3.
	async def main():
		task = asyncio.create_task(other_function())
		print(“A”)
		print(“”B”)
	async def other_function():
		print(“1”)
		await asyncio.sleep(2)
		print(“2”)
asyncio.run(main())

result A B 1

4. 

	async def main():
		task = asyncio.create_task(other_function())
		print(“A”)
		await asyncio.sleep(1)
		print(“”B”)
		
	async def other_function():
		print(“1”)
		await asyncio.sleep(2)
		print(“2”)
asyncio.run(main())

result A 1 B

5 . 
async def main():
		task = asyncio.create_task(other_function())
		print(“A”)
		await asyncio.sleep(1)
		print(“”B”)
		await task
	async def other_function():
		print(“1”)
		await asyncio.sleep(2)
		print(“2”)
asyncio.run(main())
	
result A 1 B 2

6 . 
	async def main():
		task = asyncio.create_task(other_function())
		await task
		print(“A”)
		await asyncio.sleep(1)
		print(“”B”)
		
	async def other_function():
		print(“1”)
		await asyncio.sleep(2)
		print(“2”)
asyncio.run(main())
	
result 1 2 A B

7.
	async def main():
		task = asyncio.create_task(other_function())
		print(“A”)
		await asyncio.sleep(1)
		print(“”B”)
		return_value = await task
		print(f”R {return_value}”)
		
	async def other_function():
		print(“1”)
		await asyncio.sleep(2)
		print(“2”)
		return 10
asyncio.run(main())
result A 1 B 2 R 10


[async_docs.docx](https://github.com/CODER4149/your_readme_files/files/12827709/async_docs.docx)






