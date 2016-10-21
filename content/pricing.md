+++
title = "About OLRC"
description = "About the Ontario Library Research Cloud"
draft = false
+++

# About
The Ontario Library Research Cloud (OLRC) is a project from the Ontario Council of University Libraries (OCUL) to provide cloud services for OCUL members. Currently the OLRC is synonymous with cloud storage however we’re on the path to providing other cloud services like compute services and spawning and managing Virtual Machines.
## Overview
## History

## Technology Stack
The OLRC project revolves around OpenStack (http://www.openstack.org/) technologies. Openstack provides several different software solutions that perform specific functions but are intended to work together. Currently we are using Keystone (keystone.openstack.org) for authentication and Swift (swift.openstack.org) for object storage.

A key distinction to make with the OLRC as it currently stands is that it provides Object storage. Object storage is different in the sense that it is not optimal for frequent writes or updates and is instead better for depositing data for preservation or as a distribution platform for content.

For example, the OLRC would be a good place to store backups of databases. It can also be used to supply an application with content.

### How it works under the hood
Swift is meant to be very robust and withstand downages. The OLRC is powered by 5 nodes at different participating schools. When a file is uploaded to the cloud, Swift makes 3 copies of it, guaranteeing that they are located at different nodes. The beauty of swift is that it has high tolerance for damages. For data on the cloud to be lost, it would require 3 schools to simultaneously have their servers destroyed. Even if one school has damaged servers or parts of equipment, Swift is flexible enough to be able to fully remove drives in a server and replace them. Swift will be able to replace all the files that were on that drive thanks to the extra backups at another school. It’s like a lizard that can regrow its tail.

## Participating Schools
* University of Toronto
* Ryerson University
* York University
* University of Guelph
* McMaster University
* Queen’s University
* University of Ottawa
* Carleton University
* University of Waterloo


