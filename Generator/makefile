.PHONY : clean superclean build test

default: clean build

clean:
	swift package clean

superclean:
	rm -rf .build

build:
	swift build
	.build/debug/TemplateEncoder > Source/CuckooGeneratorFramework/Templates.swift
	swift build

test: build
	cd Tests && cucumber

record: -test
	for file in .build/log/*/*.swift; do
		fileName="$(echo "$file" | awk -F"/" '{print $NF}')"
		expectedFile="Tests/SourceFiles/Expected/$fileName"
		if [ -f "$expectedFile" ]; then
			cp "$file" "$expectedFile"
		fi
	done
