# Lightstreamer Instant Messenger Demo Adapter #

This project shows the Messenger Demo Data and Metadata Adapters and how they can be plugged into Lightstreamer Server and used to feed the [Lightstreamer Basic Messenger Demo](https://github.com/Weswit/Lightstreamer-example-Messenger-client-javascript) front-end. Please refer [here](http://www.lightstreamer.com/latest/Lightstreamer_Allegro-Presto-Vivace_5_1_Colosseo/Lightstreamer/DOCS-SDKs/General%20Concepts.pdf) for more details about Lightstreamer Adapters.
The [Lightstreamer Basic Messenger Demo](https://github.com/Weswit/Lightstreamer-example-Messenger-client-javascript) is a very simple instant messenger application based on Lightstreamer.

The project is comprised of source code and a deployment example. The source code is divided into two folders.

## Messenger Adapter - src_data ##
Contains the source code for the Messenger Data Adapter. This Data Adapter provides a basic round-trip support for client-originated messages to client-specific Items.<br>

## Metadata Adapter - src_metadata ##
 Contains the source code for a Metadata Adapter to be associated with the Messenger Demo Data Adapter. This Metadata Adapter inherits from the reusable [LiteralBasedProvider](https://github.com/Weswit/Lightstreamer-example-ReusableMetadata-adapter-java) and just adds a simple support for message submission.<br>
It should not be used as a reference for a real case of client-originated message handling, as no guaranteed delivery and no clustering support is shown.

# Build #

If you want to skip the build process of this Adapter please note that in the [Deployment_LS](https://github.com/Weswit/Lightstreamer-example-Messenger-adapter-java/releases) release of this project you can find the "Deployment_LS.zip" file that contains a ready-made deployment resource for the Lightstreamer server.
Otherwise follow these steps:

*  Get the ls-adapter-interface.jar, ls-generic-adapters.jar, and log4j-1.2.15.jar files from the [latest Lightstreamer distribution](http://www.lightstreamer.com/download).
*  Create the jars LS_messenger_metadata_adapter.jar and LS_messenger_data_adapter.jar with commands like these:
```sh
 >javac -source 1.7 -target 1.7 -nowarn -g -classpath compile_libs/log4j-1.2.15.jar;compile_libs/ls-adapter-interface/ls-adapter-interface.jar;compile_libs/ls-generic-adapters/ls-generic-adapters.jar -sourcepath src/src_data -d tmp_classes src/src_data/messenger_demo/adapters/IMDataAdapter.java
 
 >jar cvf LS_messenger_data_adapter.jar -C tmp_classes src_data
 
 >javac -source 1.7 -target 1.7 -nowarn -g -classpath compile_libs/log4j-1.2.15.jar;compile_libs/ls-adapter-interface/ls-adapter-interface.jar;compile_libs/ls-generic-adapters/ls-generic-adapters.jar;LS_messenger_data_adapter.jar -sourcepath src/src_metadata -d tmp_classes src/src_metadata/messenger_demo/adapters/IMMetadataAdapter.java
 
 >jar cvf LS_messenger_metadata_adapter.jar -C tmp_classes src_metadata
```

# Deploy #

Now you are ready to deploy the Instant Messenger Demo Adapter into Lighstreamer server.<br>
After you have Downloaded and installed Lightstreamer, please go to the "adapters" folder of your Lightstreamer Server installation. You should find a "Demo" folder containing some adapters ready-made for several demo including the Messenger one, please note that the MetaData Adapter jar installed is a mixed one that combines the functionality of several demos. If this is not your case because you have removed the "Demo" folder or you want to install the Messenger Adapter Set alone, please follow these steps to configure the Messenger Adapter Set properly:

1. You have to create a new folder to deploy the Messenger adapters, let's call it "messenger", and a "lib" folder inside it.
2. Create an "adapters.xml" file inside the "messenger" folder and use a content similar to that of the file in the directory "/Deplolyment_LS/messenger" (this is an example configuration, you can modify it to your liking).
3. Copy into /messenger/lib the jars (LS_messenger_data_adapter.jar and LS_messenger_metadata_adapter.jar) created in the previous section.

Now with the "messenger" folder obtained on your behalf or with the one in the "Deployment_LS.zip" of this project, you must follow these steps:

1. Make sure you have installed Lightstreamer Server, as explained in the GETTING_STARTED.TXT file in the installation home directory.
2. Make sure that Lightstreamer Server is not running.
3. Copy the "messenger" directory and all of its files to the "adapters" subdirectory in your Lightstreamer Server installation home directory.
4. Copy the "ls-generic-adapters.jar" file from the "lib" directory of the sibling "Reusable_MetadataAdapters" SDK example to the "shared/lib" subdirectory in your Lightstreamer Server installation home directory.
5. Lightstreamer Server is now ready to be launched.

Please test your Adapter with one of the clients in the [list](https://github.com/Weswit/Lightstreamer-example-Messenger-adapter-java#clients-using-this-adapter) below.

# See Also #

## Clients using this Adapter ##

* [Lightstreamer Messenger Demo Client for JavaScript](https://github.com/Weswit/Lightstreamer-example-Messenger-client-javascript)

## Related projects ##

* [Lightstreamer Reusable Metadata Adapter in Java](https://github.com/Weswit/Lightstreamer-example-ReusableMetadata-adapter-java)
* [Lightstreamer Chat Demo Adapter](https://github.com/Weswit/Lightstreamer-example-Chat-adapter-java)
* [Lightstreamer Chat Demo Client for JavaScript](https://github.com/Weswit/Lightstreamer-example-chat-client-javascript)

# Lightstreamer Compatibility Notes #

- Compatible with Lightstreamer SDK for Java Adapters since 5.1
