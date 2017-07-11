#!/usr/bin/env groovy
 

node (env.SLAVE) {

	env.PATH=env.PATH+":/opt/gradle/bin"

stage '\u2776 Preparation (Checking out)'
	
	git url: "https://github.com/MNT-Lab/mntlab-pipeline.git", branch: 'atsuranau'
	echo "\u2600 Repo downloaded"
 

 
stage '\u2777 Building'
	
	sh 'gradle build'
	wrap([$class: 'TimestamperBuildWrapper']) {
     	echo "\u2600 Build completed"
   }

stage '\u2778 Testing'

	parallel (
		'Cucumber Tests': {sh 'gradle cucumber' },
                'Jacoco Tests': {sh 'gradle jacocoTestReport' },
                'Unit Tests': {sh 'gradle test' }
		)
	wrap([$class: 'TimestamperBuildWrapper']) {
     	echo "\u2600 Testing completed"
   }


} // node

