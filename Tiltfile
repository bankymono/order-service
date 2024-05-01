include('../catalog-service/Tiltfile')

gradlew = "./gradlew"
expected_ref = "$EXPECTED_REF"
if os.name == "nt":
  gradlew = "gradlew.bat"
  expected_ref = "%EXPECTED_REF%"

# Build
custom_build(
    # Name of the container image
    ref = 'order-service',
    # command to build the container image
    command =gradlew + ' bootBuildImage --imageName ' + expected_ref,
    # Files to watxh the trigger a new build
    deps = ['build.gradle', 'src'])

# Deploy
k8s_yaml(['k8s/deployment.yml','k8s/service.yml'])

# manage
k8s_resource('order-service',port_forwards=['9002'])