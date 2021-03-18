If there is trouble refreshing the dependencies in Eclipse after making changes to the build.gradle file, follow the steps below:

1. check if you have included eclipse gradle plugin. `apply plugin : 'eclipse'`
1. Go to your project terminal
1. Run `gradle tasks --all` to see the list of all available gradle tasks.
1. If the task `cleanEclipse` is available, run it.
1. If not, run `gradle cleanEclipseProject` and `gradle cleanEclipseClasspath` separately.
1. After that, run `gradle eclipse`
1. Go to the project in eclipse and refresh the project.

This should bring all the latest dependencies down and you should see them in the `Referenced Libraries` section.