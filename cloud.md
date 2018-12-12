# About

This document is a highly idiosyncratic collection of terms, how-tos, and cli/gui reference material.

# Amazon Web Services (AWS)

## Amazon Machine Images (AMI)

When creating, volume types have to be decided:
- Instance Store is ephemeral, part of the VM. This means it sticks around for reboots, but is destroyed with the instance. 
- Elastic Block Store (EBS) creates volumes distinct from the instance. Recommended by AWS, boots faster (may use more resources?).

## Regions

Regions are show in the UI as names, and must be referenced in the API using a region code. Some common ones:

Name  | Region
------|-------
N. CA | us-west-1
OR    | us-west-2
N. VA | us-east-1
OH    | us-east2 

# Azure

# Digital Ocean

# Google Cloud

# vSphere
