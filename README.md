# Carbyne Stack Knative Serving Multiport Patch

This repository is a fork of the [Knative Serving](https://github.com/knative/serving) 
repository. The provisioning and validation logic has been tweaked to support 
application pods that expose multiple ports simultaneously.

## Releasing

> **NOTE**: The following requires the [GitHub CLI](https://cli.github.com/) as
> a prerequisite.

The following snippet builds and publishes the patched Knative Serving Docker 
images on the GitHub Docker Registry and creates a release with the K8s resource 
manifests required for deploying the patched version of Knative Serving: 

~~~bash
export RELEASE_FOLDER="$(pwd)/release"
export VERSION=0.19.0
sed -i 's/cp "${ARTIFACTS_TO_PUBLISH}"/cp ${ARTIFACTS_TO_PUBLISH}/g' vendor/knative.dev/hack/release.sh
hack/release.sh \
  --version ${VERSION} \
  --publish \
  --release-dir "${RELEASE_FOLDER}" \
  --release-gcr ghcr.io/carbynestack/serving \
  --tag-release \
  --skip-tests
gh release create v${VERSION}-multiport-patch -n "" -p -t "Multiport Patch v${VERSION}" -R carbynestack/serving ${RELEASE_FOLDER}/*.yaml
~~~

## License

Modifications to the original Knative Serving source code are open-sourced under 
the same Apache License 2.0 as Knative Serving itself. See the [LICENSE](LICENSE) 
file for details.

## Contributing

Please see the Carbyne Stack
[Contributor's Guide](https://github.com/carbynestack/carbynestack/blob/master/CONTRIBUTING.md).