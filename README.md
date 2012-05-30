Introduction
============

A maven plugin to generate camel diagram from routes.


Screenshot
==========

[http://wiki.rmannibucau.googlecode.com/hg/images/camel.png](http://wiki.rmannibucau.googlecode.com/hg/images/camel.png)

Usage
===== 

    <build>
      <plugins>
        <plugin>
          <groupId>fr.rmannibucau</groupId>
          <artifactId>maven-diagram-generator-plugin</artifactId>
          <version>0.0.1-SNAPSHOT</version>
          <executions>
            <execution>
              <id>pack</id>
              <phase>package</phase>
              <goals>
                <goal>diagram</goal>
              </goals>
            </execution>
          </executions>
          <configuration>
            <input>src/main/resources/spring</input> <!-- or a qualified RouteBuilder name if you use java routes -->
            <view>false</view> <!-- default = false, true to show a window containing the diagram -->
            <width>480</width> <!-- default = 640  -->
            <height>640</height> <!-- default = 480 -->
            <output>target/diagram</output> <!-- default = target/diagram -->
            <type>camel</type> <!-- default = camel -->
            <fileType>xml</fileType> <!-- default = xml, other values = { java  }-->
            <format>png</format> <!-- default = png, you can set jpg ... -->
            <adjust>true</adjust> <!-- true allows to resize icons, false force to keep their original size; default: true -->
          </configuration>
          <dependencies>
            <dependency> <!-- to use camel generator -->
              <groupId>fr.rmannibucau</groupId>
              <artifactId>camel-loader</artifactId>
              <version>0.0.1-SNAPSHOT</version>
            </dependency>
            <!-- route dependencies if needed -->
          </dependencies>
        </plugin>
      </plugins>
    </build>

Advanced
======== 

You can implement your own Loader (it follows java spi) and then use it in your pom.xml (you have to put
it as dependency for your plugin).

Note
====

This plugin suppose you don't have cycles in your diagram and you have each endpoints only once. If you
use the same endpoints twice try to change a bit its name during the generation.

Nestor Notes
===========
I have forked this plugin just to allow releasing it to our maven repo. Here is the command I used for today:
  find ./ -name "*.xml" -print0 | xargs -0 perl -pi -e 's/0.0.1-SNAPSHOT/0.0.1-20120530/g' 

