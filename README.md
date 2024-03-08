# SCAP Guide

This repository contains resources for learning `Security Content Automation Protocol (SCAP)`

## Preparation

Prepare environment in docker:

    docker-compose up -d
    docker exec -it openscap bash 
    apt update && apt install -y libopenscap8

## Usage

### Policy

Check custom policy:

    oscap oval validate /mnt/policy/linux_test_config_oval.xml

    oscap info /mnt/policy/linux_test_config_oval.xml

Test policy:

    oscap oval eval \
      --results /tmp/results.xml \
      --report  /tmp/report.html \
      /mnt/policy/linux_test_config_oval.xml

Result:

    Definition oval:linux_test_config:def:1: false
    Evaluation done.

Fix and test policy:

    echo test > /tmp/test.conf
    oscap oval eval \
      --results /tmp/results.xml \
      --report  /tmp/report.html \
      /mnt/policy/linux_test_config_oval.xml

Result:

    Definition oval:linux_test_config:def:1: true
    Evaluation done.

### Benchmark

Check benchmark:

    oscap xccdf validate /mnt/policy/linux_test_xccdf.xml

    oscap info /mnt/policy/linux_test_xccdf.xml

Run:

    oscap xccdf eval /mnt/policy/linux_test_xccdf.xml

## Useful resources

[Examples of OVAL policies](https://github.com/OVALProject/Test-Content/tree/master/linux)

Get premade policies:

    apt install -y ssg-base ssg-debderived

    wget https://security-metadata.canonical.com/oval/com.ubuntu.$(lsb_release -cs).usn.oval.xml.bz2
    bzip2 -d com.ubuntu.jammy.usn.oval.xml.bz2
    oscap oval eval --report oval-jammy.html com.ubuntu.jammy.usn.oval.xml
