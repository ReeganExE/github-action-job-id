# ReeganExE/github-action-job-id

Since Github action doesn't expose job details (ID, URL) to the environment.
This action will expose those through environment variables. Just include the action step, no passing arguments!

```yml
name: "Test"
on:
  workflow_dispatch:
jobs:
  Test:
    name: This is a test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

      - uses: ReeganExE/github-action-job-id@v1.0

      - run: |
          echo $GH_JOB_0_ID
          env | grep GH_JOB

```

By default, it exposes env variables as `$GH_JOB_<JOB_INDEX>_ID`. If you want to use job name instead, add the arg `expose-name: true`.

__Note: the sepcial characters in the job name will be replaced by _ character__

```yml
name: "Test"
on:
  workflow_dispatch:
jobs:
  Test:
    name: This is a test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

      - uses: ReeganExE/github-action-job-id@v1.0
        with:
          expose-name: true

      - run: |
          echo $GH_JOB_0_ID
          echo $GH_JOB_This_is_a_test_ID
          env | grep GH_JOB
  Job2:
    name: Job2
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

      - uses: ReeganExE/github-action-job-id@v1.0
        with:
          expose-name: true

      - run: |
          echo $GH_JOB_1_ID
          echo $GH_JOB_Job2_ID
          env | grep GH_JOB
  Job3:
    name: Job3
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

      - uses: ReeganExE/github-action-job-id@v1.0
        with:
          expose-name: true

      - run: |
          echo $GH_JOB_2_HTML_URL

          # Dynamic variable
          printenv "GH_JOB_"$GITHUB_JOB"_HTML_URL"

```

# LICENSE

AGPL-3.0 License
