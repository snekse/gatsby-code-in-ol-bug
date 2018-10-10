---
title: Code in an Ordered List - Working New
date: "2018-10-09T22:12:03.284Z"
---

#New Code
Demonstrate a gatsby bug when there is a code block in an ordered list.


**How to use**

1.  Copy this script into the root of your Terraform project directory(ies) as a file named **terraformw**.

    ```bash
    #!/bin/bash

    TERRAFORM_VERSION="0.11.1"

    if [ -z ${TERRAFORM_BIN_PATH+x} ]; then
    	TERRAFORM_BIN_PATH="$HOME/.terraform";
    fi

    platform='unknown'
    unamestr=`uname`
    if [[ "$unamestr" == 'Linux' ]]; then
       platform='linux'
    elif [[ "$unamestr" == 'FreeBSD' ]]; then
       platform='freebsd'
    elif [[ "$unamestr" == 'Darwin' ]]; then
       platform='darwin'
    fi

    arch="unknown"
    unamestr=`uname -m`
    if [[ "$unamestr" == 'x86_64' ]]; then
       arch='amd64'
    elif [[ "$unamestr" == 'i686' ]]; then
       arch='386'
    fi

    TERRAFORM_URL="https://releases.hashicorp.com/terraform/$TERRAFORM_VERSION/terraform_$TERRAFORM_VERSION"_"$platform"_"$arch".zip

    TERRAFORM_PATH="$TERRAFORM_BIN_PATH/$TERRAFORM_VERSION"
    TERRAFORM_CMD="$TERRAFORM_PATH/terraform"
    if ! type "$TERRAFORM_CMD" > /dev/null 2>&1; then
    	echo "Downloading $TERRAFORM_URL"
    	mkdir -p "$TERRAFORM_PATH"
    	curl -s "$TERRAFORM_URL" -o $TERRAFORM_PATH.zip
    	cd $TERRAFORM_PATH && unzip $TERRAFORM_PATH.zip && cd -
    fi

    $TERRAFORM_CMD $@

    #
    ```

2.  Update the TERRAFORM\_VERSION variable to match the version of Terraform you are using.
3.  Give the script executable permissions (**chmod +x terraformw**)
4.  Run it instead of the **terraform** executable: **./terraformw plan -out plan.out**
5.  Commit the file to source control

There you have it! This is a pretty simple script ...