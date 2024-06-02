---
title: "Install and configure Encly"
date: 2019-12-18T15:44:46+06:00
type: portfolio
image: "logo.jpg"
category: "GUIDE"
tags: ["GUIDE"]
toc: true
project_images: ["images/projects/project-details-image-one.jpg", "images/projects/project-details-image-two.jpg"]
---

> This guide explains how to install a fictitious software product, “Encly”. Encly is based on a real much larger product I documented, though many details have changed in this document. I wrote the original document in asciidoc and it was published using Antora.

# Install and configure Encly

See [Encly documentation](internal-link.com) for details about the component and its architecture.

## Prerequisites

To install Encly you must run an [Ansible playbook](https://docs.ansible.com/ansible/latest/userguide/playbooks.html). This can be done by accessing the `os-operator` pod in the `os-ops` namespace.

Execute the following statement:

    keos play /acme/ansible/playbooks/system-services/encly.yml -e encly_namespace=encly -e encly_service=encly

## Step 1: Installation

To install Encly follow these steps:

1. Access the Application Center via `https://${external_domain}/ac` and log in with the new tenant's credentials (for this example, "encly-user" user and "encly-tenant" tenant).
2. Access the catalog by clicking "Marketplace" in the navigation menu. Search for "Encly" in the search box on your right and click on the corresponding box.

3. Select a version and click "Deploy".

4. Next, you will see the pre-deployment form:
    1. Select the namespace "encly".
    2. In "PostgreSQL used for connection" select "pool-psql".
    3. In "PostgreSQL used for policy[...]" select "psql.acme-datastores".
    4. In "HDFS used for connection" select "hdfs.acme-datastores".
    5. In this section, you can configure placements and priority classes for multiuser and analytic environments and for Spark executors.

5. Click "Continue".
6. Next, you will see the descriptor. The default _Service ID_ is "encly".
    1. Go to the 'Users authentication and authorization' section:
        1. In "Security Layer group" add "encly".
        2. In "Users with admin Role" add "acme".
    2. Click "Deploy".

## Step 2: Permission settings

In order to configure Encly’s permissions you must create a custom group for Encly.

1. Access the security layer via `https://${external_domain}/sec` and log in with the new tenant's credentials (for this example, "acme" user and "acme" tenant).
2. Go to 'Identities' in the navigation menu and 'Groups' in the menu below it. Click "Create a custom Group" as shown in the image.

3. Add the new group's name, for this example `encly`, and click "Save".

4. Back on the previous page, select "Users" from the side menu and click "Edit users" as shown in the image.

5. In the modal window, click on the checkbox of the user you want to add, in this case, "acme". Click "Edit".

With these steps, you have managed to associate the permissions of the new user to the Encly component.

## Step 3: Verification

To check that the installation has been executed correctly, follow these steps:

1. Access Encly via `https://encly.${tenant}.${external_domain}/encly` (e.g. `https://encly.acme.example.com/encly`) with your credentials.
2. Click "Start My Server".

    1. After logging in, you will see the image below. This means that an analytical environment is being generated for the chosen user.

3. You are now able to see the analytical environment interface.

4. Create an example of a PySpark notebook and execute these commands to test the access to Encly's catalog.

````
   from pyacme.dx.dxsession import DXSession
   dx = DXSession(sc)
   dx.sql("SHOW TABLES").show()
   dx.sql("SELECT * FROM test").show()
````
