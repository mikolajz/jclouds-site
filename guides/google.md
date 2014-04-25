---
layout: page
title: "Google Cloud Platform: Getting Started Guide"
permalink: /guides/google/
---

1. [Introduction](#intro)
2. [Authentification](#auth)
2. [Running examples](#examples)


## <a id="intro"></a>Introduction
This guide helps you to get started with [Google Cloud Platform](https://cloud.google.com/) development using jclouds.

Currently, [Google Compute Engine](https://developers.google.com/compute/) is covered. This is a service that allows you to run vitual machines on Google's infrastructure.

This guide assumes you have a Google Cloud project. If not yet, you can sign up on the [Developer Console](https://console.developers.google.com/). For GCE, you need to set up billing.

## <a id="auth"></a>Authentification
Google Cloud Platform uses OAuth which gives a variety of choices how to authentificate:
  * One can ask a user for consent to perform operations in his/her name.
  * One can create a service account and use its private key to authentificate.
  * Unless configured otherwise, programs running on a GCE instance can perform operations as the project's default service account ([documentation](https://developers.google.com/compute/docs/authentication)).

You can find all the details in [the documentation](https://developers.google.com/accounts/docs/OAuth2), while in these examples we will focus only on service accounts (bullet 2).

To create a new service account:
  * Go to the [Developer Console](https://console.developers.google.com/).
  * Choose API & auth > Credentials.
  * Click "Create new Client ID".
  * Select "Service account" and click "Create service ID".
  * Data about the new service account will be visilble in the console and a private key will be downloaded. Notice that the data includes service account email address - you will need it to use the account.
  * To keep the examples simple, we use private keys without passwords. It might be something you will not do in a production environment, but for the examples run: `openssl pkcs12 -in {downloaded_file}.p12 -nodes -out gcp-example.pem  -passin pass:notasecret`.

## <a id="examples"></a>Running examples
A good starting point is to run examples programs. For this, download the [jclouds-example](https://github.com/jclouds/jclouds-examples) repository and build the "google" Maven project. Each example can be run by passing the service account email as the first parameter and the path to the gcp-example.pem file (created by removing the password from the *.p12 file by the command above) as the second.

For example, running [org.jclouds.examples.google.computeengine.CreateServer](https://github.com/jclouds/jclouds-examples/blob/master/google/src/main/java/org/jclouds/examples/google/computeengine/CreateServer.java) will create a new virtual machine running Debian (and its persistent disk). Open the [Developer Console](https://console.developers.google.com/) and navigate to your project and choose "Compute Engine" to see it. You can use gcutil from Google Cloud SDK to ssh to that machine - see the SSH button on that page.

If anything failed, you can see the operation status on Compute Engine > Operations page of the [Developer Console](https://console.developers.google.com/).
