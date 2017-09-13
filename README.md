# day256
Поздравляю всех программистов с Днем Программиста!

```{r, engine='bash', count_lines}
if [ $(date +%j) -eq 256 ] ; then echo ; for i in {2..11} ; do printf "$(bc <<< "obase=2;$i")" ; done ; echo ; echo 'Ta-da! Day of the Programmer!' ; for i in {2..11} ; do printf "$(bc <<< "obase=2;$i")" ; done ; echo ; echo ; else if [ $(date +%j) -lt 256 ] ; then echo "$(bc <<< "obase=2;$(( 256 - $(date +%j) ))") day(s) left"; else if [ $(( $(date +%Y) % 5 )) -eq 0 ] ; then echo "$(bc <<< "obase=2;$(( 622 - $(date +%j) ))") day(s) left" ; else echo "$(bc <<< "obase=2;$(( 621 - $(date +%j) ))") day(s) left" ; fi ; fi ; fi
```

Если вы не любите bash, вот несколько строк, которые сделают вам проект java приложения, скомпилируют и выполнят его.
Просто запишите их в файл day256.sh и выполните в консоли Линукс или GitBash в Windows.

```{r, engine='bash', count_lines}
#!/bin/bash

mvn archetype:generate -DgroupId=ru.lumo.day256 -DartifactId=day256 -DachetypeArtifactId=maven-achetype-quickstart -DinteractiveMode=false > /dev/null 2>&1
cd day256/
echo -e 'package ru.lumo.day256;\n\nimport java.util.Calendar;\n\n/**\n * Day of the Programmer\n */\npublic class App {\n    public static void main(String[] args) {\n        int dayOfYear = Calendar.getInstance().get(Calendar.DAY_OF_YEAR);\n        if (dayOfYear == 256) System.out.println("Ta-da! Day of the Programmer!");\n        else if (dayOfYear < 256) System.out.println((256 - dayOfYear) + " day(s) left");\n        else System.out.println((621 - dayOfYear) + " day(s) left");\n    }\n}\n' > ./src/main/java/ru/lumo/day256/App.java
echo -e 'package ru.lumo.day256;\n\nimport org.junit.Assert;\nimport org.junit.Test;\n\nimport java.io.ByteArrayOutputStream;\nimport java.io.PrintStream;\nimport java.io.UnsupportedEncodingException;\n\n/**\n * Unit test for Day of the Programmer.\n */\npublic class AppTest {\n\n    @Test\n    public void testApp() throws UnsupportedEncodingException {\n        ByteArrayOutputStream baos = new ByteArrayOutputStream();\n        System.setOut(new PrintStream(baos));\n        App.main(new String[]{});\n        String s = new String(baos.toByteArray(), "utf-8");\n        Assert.assertTrue(s.length() > 1);\n    }\n}\n' > ./src/test/java/ru/lumo/day256/AppTest.java
cat pom.xml| sed 's/<scope>test<\/scope>/<\!--<scope>test<\/scope>-->/g' |sed 's/<version>3.8.1<\/version>/<version>4.12<\/version>/g' |sed 's/<\/project>//g' > pom2.xml
echo -e '\n\n    <build>\n        <plugins>\n            <plugin>\n                <groupId>org.apache.maven.plugins</groupId>\n                <artifactId>maven-jar-plugin</artifactId>\n                <configuration>\n                    <archive>\n                        <manifest>\n                            <addClasspath>false</addClasspath>\n                            <mainClass>ru.lumo.day256.App</mainClass>\n                        </manifest>\n                    </archive>\n                </configuration>\n            </plugin>\n        </plugins>\n    </build>\n\n</project>\n' >> pom2.xml
mv pom.xml pom.old
mv pom2.xml pom.xml
mvn clean install > /dev/null 2>&1
java -jar ./target/day256-1.0-SNAPSHOT.jar
```

Перед запуском убедитесь, что установлены java (java -version) и maven (mvn -version).
