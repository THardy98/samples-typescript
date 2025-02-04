### Go
---
```
// Send an email every 30 days
func SleepForDaysWorkflow(ctx workflow.Context) (string, error) {
  for {
    workflow.ExecuteActivity(ctx, SendEmail) // Activities have timeouts, and will be retried by default!
    workflow.Sleep(ctx, time.Hour*24*30) // Sleep for 30 days!
  }
  // ...
}
```

### Java
---
```
public class SleepForDaysImpl implements SleepForDaysWorkflow {
  // Send an email every 30 days
  public String sleepForDays() {
    while (true) {
      activity.sendEmail(); // Activities have timeouts, and will be retried by default!
      Workflow.sleep(Duration.ofDays(30)); // Sleep for 30 days!
    }
    // ...  
  }
}
```

### Typescript
---
```
// Send an email every 30 days
export async function sleepForDays(): Promise<void> {
  while (true) {
    await sendEmail(); // Activities have timeouts, and will be retried by default!
    await workflow.sleep('30 days') // Sleep for 30 days!
  }
  // ...
}
```

### Python
---
```
@workflow.defn()
class SleepForDaysWorkflow:
    // Send an email every 30 days
    @workflow.run
    async def run(self) -> None:
        while true:
            // Activities have timeouts, and will be retried by default!
            await workflow.execute_activity(
                send_email,
                start_to_close_timeout=timedelta(seconds=10),
            )
            workflow.sleep(timedelta(days=30)) // Sleep for 30 days!
        // ...
```

### .Net
---
```
[Workflow]
public class SleepForDaysWorkflow
{
    // Send an email every 30 days
    [WorkflowRun]
    public async Task RunAsync()
    {
        while (true)
        {
            // Activities have timeouts, and will be retried by default!
            await Workflow.ExecuteActivityAsync(
                (Activities act) => act.SendEmail(),
                new() { StartToCloseTimeout = TimeSpan.FromSeconds(10) });
            Workflow.DelayAsync(TimeSpan.FromDays(30)); // Sleep for 30 days!
        }
        // ...
    }
}
```
