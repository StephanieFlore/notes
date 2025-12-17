classDiagram
    class JobSystem {
      +CreateOrGet() JobSystem*
      +Destroy() void
      +CreateWorkerThread(uniqueName, workerJobChannels=0xFFFFFFFF) void
      +DestroyWorkerThread(uniqueName) void
      +QueueJob(job: Job*) void
      +ClaimAJob(workerJobChannels) Job*
      +GetJobStatus(jobID) JobStatus
      +IsJobComplete(jobID) bool
      +OnJobCompleted(job: Job*) void
      +FinishCompletedJobs() void
      +FinishJob(jobID) void
    }

    class JobWorkerThread {
      -m_uniqueName
      -m_workerJobChannels
      +Run() void
    }

    class Job {
      <<abstract>>
      +Execute() void
      +JobCompleteCallback() void
      +GetUniqueID() int
      -m_jobID : int
      -m_jobType : int
      -m_jobChannels : unsigned long
    }

    class CompileJob {
      +returnCode : int
      +output : string
      +Execute() void
      +JobCompleteCallback() void
    }

    class ParseJob {
      +compileJobID : int
      +Execute() void
      +JobCompleteCallback() void
    }

    JobSystem "1" o-- "*" JobWorkerThread : owns
    JobSystem "1" o-- "*" Job : queues/tracks
    JobWorkerThread --> JobSystem : claims jobs from
    CompileJob --|> Job
    ParseJob --|> Job

