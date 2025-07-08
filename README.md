Reproducer for Maven 4.0.0-rc-4 profile activation bug
======================================================

    $ ./mvnw -q wrapper:wrapper -Dmaven=3.9.9 && ./mvnw validate | grep "Profile activated"
    [WARNING]      [echo] Profile activated in my-app: Test 1
    [WARNING]      [echo] Profile activated in my-lib: Test 2

Show that profile is activated in both parent and child project

    $ ./mvnw -q wrapper:wrapper -Dmaven=4.0.0-rc-4 && ./mvnw validate | grep "Profile activated"
    [WARNING]      [echo] Profile activated in my-app: Test 1

With Maven 4 RC, the profile is only activated in parent project, even if

    $ ./mvnw -q wrapper:wrapper -Dmaven=4.0.0-rc-4 && ./mvnw -q help:all-profiles -Doutput=/dev/pts/0
    Listing Profiles for Project: com.mycompany.app:my-app:pom:1.0-SNAPSHOT
        Profile Id: test (Active: true, Source: pom)
    Listing Profiles for Project: com.mycompany.app:my-lib:jar:1.0-SNAPSHOT
        Profile Id: test (Active: true, Source: pom)

shows profile to be active in both
