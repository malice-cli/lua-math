```lua
function fwait(n)
    task.desynchronize()
    local n = n or 1/600
	local thread = coroutine.running();
	local start = os.clock();
	task.delay(n,function()
		task.defer(thread,start)
	end)
	local now = coroutine.yield()
	task.synchronize()
	return now-start, elapsedTime()
end
```
**THIS FUNCTION IS EXPLOITABLE**

This function takes in a time `n` in seconds and waits for that amount of time before continuing. It does this by calculating the end time using the current time and the desired wait time, and then entering a loop that continues until the current time is greater than the end time.

To make the function more efficient, it yields control to other tasks during each iteration of the loop using the `coroutine.yield()` function. This allows other tasks to run while the wait function is waiting, which can help prevent the game from becoming unresponsive.

In the example above, the `wait(5)` call will cause the script to wait for 5 seconds before continuing. This can be useful for adding delays between actions or animations in a game.




