# Synthea™ Custom Exporter Template

The Synthea Custom Exporter Template is intended to help you create your own Synthea patient exporter without having to modify Synthea directly. A small example of using this template to write patients to a Postgres database is available at: https://github.com/dehall/example-exporter-postgres


## Setup and Creating a JAR file

This template contains the following files which may be altered for your needs:

- `build.gradle`: If you require any software libraries not already included in Synthea, they can be added here. See the notes in this file for the proper way of adding libraries.

- `settings.gradle`: Change the name "custom-exporter-template" to whatever you like, this will only affect the name of the final JAR file.

- `src/main/java/org/mitre/synthea/exporters/`
  - `SamplePatientExporter.java`: This file contains the implementation of a Patient exporter, which is called for every Patient in a run of Synthea. 
  - `SamplePostCompletionExporter.java`: This file contains the implementation of a post-completion exporter, which is called once at the end of a run of Synthea. Note that the method in this class does not receive the Patient instances. 
  - These two files are the primary entry point and this is where you should add your code, or call another library.
  - These two files may both be moved around and renamed freely. If you do, make sure to update the references to them in the files below. If you only need one of the two types of exporter, you may delete this file and its corresponding service file below.

- `src/main/resources/META-INF/services/`
  - `org.mitre.synthea.export.PatientExporter`: This file points to the location of all classes that implement the PatientExporter interface. If you create multiple classes that implement this interface, make sure to add them here.
  - `org.mitre.synthea.export.PostCompletionExporter`: This file points to the location of all classes that implement the PostCompletionExporter interface. If you create multiple classes that implement this interface, make sure to add them here.


Once your code is ready, run the following command to produce the jar file:
```sh
./gradlew jar
```

The jar file will be created in `./build/libs/`.

## Usage
For the basics of running Synthea, please refer to [Basic Setup and Running](https://github.com/synthetichealth/synthea/wiki/Basic-Setup-and-Running)
or [Developer Setup and Running](https://github.com/synthetichealth/synthea/wiki/Developer-Setup-and-Running) on the Synthea wiki.

If you are using the "Basic Setup" of Synthea, add your .jar file to the classpath and run Synthea as follows:


```sh
java -jar synthea-with-dependencies.jar -cp path/to/custom-exporter-template.jar
```

Other options may be appended to the end of the command as usual.


If you are using the "Developer Setup" of Synthea, add your .jar to its `./lib/custom/` directory, and run synthea with `./run_synthea`, with other options appended to the end of the command as usual.

## License

Copyright 2023 The MITRE Corporation

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
