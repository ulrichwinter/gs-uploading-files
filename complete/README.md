This is a demo project to reproduce the following issue within spring boot:
https://github.com/spring-projects/spring-boot/issues/7735

It is a modified version of the spring boot guide for multipart file upload:
https://github.com/spring-guides/gs-uploading-files

The difference is, that the commons fileupload is used instead of the implicitly configured servlet 3 variant.

The error is, that the multipart parsing fails therfore the multipart request parameter is not found.
This is reproducible with spring boot 2.0.2.RELEASE.
It occured in my production project with 1.5.12.RELEASE, too - but was not reproducable w in this demo with that boot release.

The workaround is 
- to disable auto configuration of MultipartAutoConfiguration (see commented out part in hello.Application.java)
- or to use servlet 3.0 multipart handling by not configuring the CommonsMultipartResolver (i.e. remove the MultipartResolverConfiguration completely)


There are two stacktrace included (captured when running the test hello.FileUploadIntegrationTests.shouldUploadFile):

- one just before the exception occures within common fileuploads MultipartStream.skipPreamble:
(see file stacktrace-just-before-exception.txt)
- one when the exception is handled by finishing parsing at all 
(see file stacktrace-handling-exception.txt)
  
