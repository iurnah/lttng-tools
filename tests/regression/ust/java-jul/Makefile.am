
noinst_SCRIPTS = test_java_jul JTestLTTng.java
EXTRA_DIST = test_java_jul JTestLTTng.java

if HAVE_JAVA_JDK
JCC=$(JAVA_JDK)/bin/javac
else
JCC=javac
endif

AGENT_JAR_FILE=$(java_agent_jar_path)


# Still need to copy test files in case of out of tree build
if BUILD_JAVA_AGENT
all-local: static_file JTestLTTng.class
%.class: %.java
	$(JCC) -d "$(builddir)" -cp "$(AGENT_JAR_FILE):." $<
else
all-local: static_file
endif # BUILD_JAVA_AGENT


static_file:
	@if [ x"$(srcdir)" != x"$(builddir)" ]; then \
		for script in $(EXTRA_DIST); do \
			cp -f $(srcdir)/$$script $(builddir); \
		done; \
	fi


clean-local:
	rm -f *.class
	@if [ x"$(srcdir)" != x"$(builddir)" ]; then \
		for script in $(EXTRA_DIST); do \
			rm -f $(builddir)/$$script; \
		done; \
	fi

