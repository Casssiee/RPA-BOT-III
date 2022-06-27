# Template: Standard Robot Framework

The insurance sales system API has some quirks. It has a relatively slow response time. Also, sometimes it fails to process the submitted data, returning exceptions. In addition, bombarding it with too many payloads too fast will bring the whole system down. Since the processing might be very slow, and there might be API requests that need to be retried later after a long enough waiting time (so as not to crash the API), I decide to implement the robot using the producer-consumer pattern. That pattern will enable me to build the automation in a way that allows me to track the status of individual requests and mitigates the risk of everything falling apart!In practice, the robot will use work items. One task is to generate the sales system API payload from the raw traffic data (the input). The other is to process that data and submit it to the insurance sales system.
----------------
┌──────────┐   ┌────────────┐   ┌──────────┐
│ Producer │ → │ Work items │ → │ Consumer │ → 💰
└──────────┘   └────────────┘   └──────────┘
-------------------
The failed entries will need to be retried later or edited and fixed manually in case of business exceptions.
