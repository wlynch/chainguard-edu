---
title: "Overview"
type: "article"
description: "Chainguard Images Overview"
lead: "A primer on Chainguard Images and the distroless approach"
date: 2022-09-01T08:49:31+00:00
lastmod: 2022-09-01T08:49:31+00:00
draft: false
images: []
menu:
  docs:
    parent: "chainguard-images"
weight: 100
toc: true
---

Chainguard Images is a collection of container images designed for minimalism and security.

Many of the images are distroless; they contain only an application and its runtime dependencies. These images do not even contain a shell or package manager.

Most of the images are built with [Wolfi](/open-source/wolfi/getting-started-with-wolfi), our Linux _undistro_ designed from the ground up to produce container images that meet the requirements of a secure software supply chain.

Main features include:

- Minimalist design, no bloating from unnecessary software
- Build-time SBOMs (software bill of materials) attesting the provenance of all artifacts within the image
- Verifiable signatures provided by [Sigstore](/open-source/sigstore/cosign/an-introduction-to-cosign/)
- Automated nightly builds to ensure images are completely up-to-date and contain all available security patches

Chainguard Images are available [on Github](https://github.com/chainguard-images) and the `cgr.dev` registry.

## Why Distroless

[Distroless images](https://blog.chainguard.dev/minimal-container-images-towards-a-more-secure-future/) are the result of pushing minimalism in containers to the next level. When compared to traditional base images such as [alpine](https://hub.docker.com/_/alpine) or [debian](https://hub.docker.com/_/debian), they are more stripped back, lacking even a shell or package managers. However, compared to the empty “scratch” image, they do contain structure essential for the majority of Linux applications such as root certificates for TLS and core files like `/etc/passwd`.

The major advantage of distroless images is the reduced size and complexity, which results in a vastly reduced attack surface. This is evidenced by the results from security scanners, which detect far fewer potential vulnerabilities in Chainguard Images. The following graph shows a comparison between the official Nginx image and Chainguard's Nginx image, based on the number of CVEs (common vulnerabilities and exposures) detected by Trivy:

{{< rumble left="nginx:latest" right="distroless.dev/nginx:latest" >}}