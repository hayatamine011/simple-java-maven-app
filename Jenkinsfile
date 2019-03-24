def qualitygate
podTemplate( 
    label: 'kubernetes', 
    containers: [ 
        containerTemplate(name: 'maven', image: 'maven:3.6.0-jdk-11', ttyEnabled: true, command: 'cat'), 
        containerTemplate(name: 'golang', image: 'golang:alpine', ttyEnabled: true, command: 'cat') 
    ] 
) { 
    node('kubernetes') { 
        container('maven') { 
            
            stage('build ') {
            
                // Optionally use a Maven environment you've configured already
                sh 'mvn clean package -DskipTests'


        
        }} 
    } 
}
