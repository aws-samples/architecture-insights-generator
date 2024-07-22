# Architecture Insights Generator
<img src="/ChimeraUI.png" alt="ChimeraUI" width="300">
Architecture Insights Generator is a program designed to streamline the process of analyzing AWS Trusted Adviser (TA) reports and registering identified risks into a Well-Architected (WA) workload created through a specified Custom Lens. 

## Key features:

1. Local deployment: Runs directly on a Mac, easy and convenient
2. Not limited to whether there is enterprise support service, just use the TA report export from AWS Trusted Adviser console.
3. Automatically generates a readable Excel file.
4. Automatically updates WA workload notes.

## Usage 1: Generate TA check report

1. Ensure you have a Python 3 environment with a version not lower than Python 3.12.2.
2. Install the required dependencies by running `pip install -r requirements.txt`.
3. Execute the program by running `python3 WA.py`.
4. Import the XLSX file exported from the AWS Trusted Adviser service.
5. Upon successful execution, the analysis results will be output to the `TA-check.xlsx` file in the current directory.
6. Refer to the `TA-check.xlsx` file and manually create/modify the workload in the WA Tool accordingly.

## Usage 2: Update to AWS WA Tool
The "Usage 1: Generate TA check report" needs to be completed first.

Before using this feature, you need to set up [Configuration and Credential File Settings](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html).

### IAM policy suggestion
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "wellarchitected:ListWorkloads",
                "wellarchitected:GetAnswer",
                "wellarchitected:UpdateAnswer",
                "wellarchitected:ListLenses"
            ],
            "Resource": "<YOUR RESOURCE ARN>"
        }
    ]
}

```

After setting up your [Configuration and Credential File Settings](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html), you can click on the "Setting" option in this application to configure the Region, Workload, and Lens. Once you have successfully imported the exported XLSX files from the AWS Trusted Adviser service, you can perform the "Update Workload" operation.

**The logic for updating WA notes**: It aims to preserve as much historical log in the notes as possible, with the most recent updates placed at the top. Due to the 2048 character limit, only the latest 2000 characters of the log will be retained.

If you encounter any issues, please report them in the "Issues" section of this repository.


## Supported Custom Lens

When lens.json changes, it needs to be processed by the pjson.py program to generate a new output.csv file.

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.

