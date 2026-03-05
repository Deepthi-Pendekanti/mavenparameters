# mavenparameters
Step 1 — Create GitHub Repository

Create repository:

pipeline-addition
Step 2 — Add Python Script in GitHub

Click

Add File → Create new file

File name:

add.py

Paste this code:

import sys

def add_numbers(a, b):
    return a + b

if __name__ == "__main__":
    num1 = int(sys.argv[1])
    num2 = int(sys.argv[2])

    result = add_numbers(num1, num2)

    print("=================================")
    print("Addition Result")
    print("=================================")
    print(f"First Number : {num1}")
    print(f"Second Number: {num2}")
    print(f"Sum : {result}")

Commit the file.

Step 3 — Check Python in Your System

Open CMD and run:

python --version

Example output:

Python 3.11

If Python is not installed → Jenkins cannot run the script.

 Step 4 — Create Jenkins Pipeline Job

Open Jenkins:

http://localhost:8080

Click

New Item

Enter name:

PYTHON-ADDITION

Select:

Pipeline

Click OK

Step 5 — Add Pipeline Script

Scroll to Pipeline → Script

Paste this pipeline:

pipeline {

    agent any

    parameters {

        string(name: 'BRANCH_NAME',
        defaultValue: 'main',
        description: 'Git branch')

        string(name: 'NUM1',
        defaultValue: '10',
        description: 'First Number')

        string(name: 'NUM2',
        defaultValue: '20',
        description: 'Second Number')

    }

    stages {

        stage('Checkout') {
            steps {
                git branch: "${params.BRANCH_NAME}",
                url: 'https://github.com/YOUR_USERNAME/pipeline-addition.git'
            }
        }

        stage('Addition Build') {
            steps {
                bat "python add.py ${params.NUM1} ${params.NUM2}"
            }
        }

    }

}

Replace:

YOUR_USERNAME

with your GitHub username.

Click Save.

 Step 6 — Run the Pipeline

Now Jenkins will show:

Build with Parameters

Click it.

You will see inputs:

BRANCH_NAME = main
NUM1 = 10
NUM2 = 20

Change values if needed.

Example:

NUM1 = 25
NUM2 = 15

Click Build.

Step 7 — Check Console Output

Click the build → Console Output

You will see something like:

=================================
Addition Result
=================================
First Number : 25
Second Number: 15
Sum : 40

Build result:

Finished: SUCCESS
