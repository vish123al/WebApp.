def TicketNumber

def gitCommit() {
    sh "git rev-parse HEAD > GIT_COMMIT"
    def gitCommit = readFile('GIT_COMMIT').trim()
    sh "rm -f GIT_COMMIT"
    return gitCommit
}

node {
  
    // Checkout source code from Git...change diff......
   
    stage 'Checking out scm for repository and Creating Ticket In Service Now'
        checkout scm
        sh "pip install requests"
        def output=sh (returnStdout: true, script: "python Integration.py --action Create -b ${env.BUILD_TAG}" )
        TicketNumber="${output}"
        def comment="Checkout source code from Git stage is completed"
        def result = sh(returnStdout:true , script: """python Integration.py --action Update -b ${env.BUILD_TAG} -t ${TicketNumber} -c ' ${comment} '""").trim()
        
   stage '(TEST) unit/integration testing'
    checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '**/checkstyle-result.xml', unHealthy: ''
    dry canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '**/cpd.xml', unHealthy: ''
    findbugs canComputeNew: false, defaultEncoding: '', excludePattern: '', healthy: '', includePattern: '', pattern: '**/findbugs.xml', unHealthy: ''
    pmd canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '**/pmd.xml', unHealthy: ''
    warnings canComputeNew: false, canResolveRelativePaths: false, categoriesPattern: '', consoleParsers: [[parserName: 'PHP Runtime']], defaultEncoding: '', excludePattern: '', healthy: '', includePattern: '', messagesPattern: '', parserConfigurations: [[parserName: 'PHP Runtime', pattern: '.php']], unHealthy: '' 
    //sh 'curl -X POST -H "Content-Type: application/json" http://172.29.133.15:8080/v2/apps -d@msql.json'
    //def comment=sh (returnStdout: true, script: 'curl -X POST -H "Content-Type: application/json" http://172.29.133.15:8080/v2/apps -d@msql.json' )
    //def result = sh(returnStdout:true , script: """python Integration.py --action Update -b ${env.BUILD_TAG} -t ${TicketNumber}  -c '${comment}'""").trim()
    //sh 'make test'
    //def comment=sh (returnStdout: true, script: 'make test' )
    //def result = sh(returnStdout:true , script: """python Integration.py --action Update -b ${env.BUILD_TAG} -t ${TicketNumber}  -c '${comment}'""").trim()
    comment="(TEST) unit/integration testing is completed."
    result = sh(returnStdout:true , script: """python Integration.py --action Update -b ${env.BUILD_TAG} -t ${TicketNumber}  -c '${comment}'""").trim()
    
    stage '(BUILD) building image'
    
    sh "docker build -t vishaldenge/php10:${gitCommit()} ."
    //def comment=sh (returnStdout: true, script: "docker build -t vishaldenge/php10:${gitCommit()} ." )
    //def result = sh(returnStdout:true , script: """python Integration.py --action Update -b ${env.BUILD_TAG} -t ${TicketNumber}  -c '${comment}'""").trim()
    
    sh "docker login -u vishaldenge -p 'v!sh@l123' "
    //def comment=sh (returnStdout: true, script: "docker login -u vishaldenge -p 'v!sh@l123'" )
    //def result = sh(returnStdout:true , script: """python Integration.py --action Update -b ${env.BUILD_TAG} -t ${TicketNumber}  -c '${comment}'""").trim()
    
    sh "docker login -u vdenge -p 'v!sh@l123' "
    //def comment=sh (returnStdout: true, script: "docker login -u vdenge -p 'v!sh@l123'" )
    //def result = sh(returnStdout:true , script: """python Integration.py --action Update -b ${env.BUILD_TAG} -t ${TicketNumber}  -c '${comment}'""").trim()
    
    sh "docker pull aquasec/scanner-cli:3.0"
    //def comment=sh (returnStdout: true, script: "docker pull aquasec/scanner-cli:3.0" )
    //def result = sh(returnStdout:true , script: """python Integration.py --action Update -b ${env.BUILD_TAG} -t ${TicketNumber}  -c '${comment}'""").trim()
    
    sh "docker login -u vishaldenge -p 'v!sh@l123' "
    //def comment=sh (returnStdout: true, script: "docker login -u vishaldenge -p 'v!sh@l123' " )
    //def result = sh(returnStdout:true , script: """python Integration.py --action Update -b ${env.BUILD_TAG} -t ${TicketNumber}  -c '${comment}'""").trim()
    
    sh "docker push vishaldenge/php10:${gitCommit()}"
    //def comment=sh (returnStdout: true, script: "docker push vishaldenge/php10:${gitCommit()}" )
    //def result = sh(returnStdout:true , script: """python Integration.py --action Update -b ${env.BUILD_TAG} -t ${TicketNumber}  -c '${comment}'""").trim()
    
    sh "docker pull vishaldenge/php10:${gitCommit()}"
    //def comment=sh (returnStdout: true, script: "docker pull vishaldenge/php10:${gitCommit()}" )
    //def result = sh(returnStdout:true , script: """python Integration.py --action Update -b ${env.BUILD_TAG} -t ${TicketNumber}  -c '${comment}'""").trim()
    
    aqua hideBase: false, hostedImage: '', localImage: "vishaldenge/php10:${gitCommit()}", locationType: 'local', notCompliesCmd: '', onDisallowed: 'ignore', register: false, registry: 'Docker Hub', showNegligible: false
    
    comment="(BUILD) building image stage is completed"
    result = sh(returnStdout:true , script: """python Integration.py --action Update -b ${env.BUILD_TAG} -t ${TicketNumber}  -c '${comment}'""").trim()
    
    stage '(PUBLISH) Pushing the image '
    
    sh "docker push vishaldenge/php10:${gitCommit()}"
    
    //def comment=sh (returnStdout: true, script: "docker push vishaldenge/php10:${gitCommit()}" )
    //def result = sh(returnStdout:true , script: """python Integration.py --action Update -b ${env.BUILD_TAG} -t ${TicketNumber}  -c '${comment}'""").trim()
    
    comment="(PUBLISH) Pushing the image stage is completed"
    result = sh(returnStdout:true , script: """python Integration.py --action Update -b ${env.BUILD_TAG} -t ${TicketNumber}  -c '${comment}'""").trim()
    
    
    stage '(DEPLOY) Deploying the container'
       //sh 'curl -X POST -H "Content-Type: application/json" http://mesomaster02.production.hec.local:8080/v2/groups -d@marathon2.json'
        //def comment=sh (returnStdout: true, script: 'curl -X POST -H "Content-Type: application/json" http://mesomaster02.production.hec.local:8080/v2/groups -d@marathon2.json' )
        //def result = sh(returnStdout:true , script: """python Integration.py --action Update -b ${env.BUILD_TAG} -t ${TicketNumber}  -c '${comment}'""").trim()
        
       // sh 'curl -X POST -H "Content-Type: application/json" http://10.0.1.85:8080/v2/apps -d@marathon.json'
        //def comment=sh (returnStdout: true, script: 'curl -X POST -H "Content-Type: application/json" http://10.0.1.85:8080/v2/apps -d@marathon.json' )
        //def result = sh(returnStdout:true , script: """python Integration.py --action Update -b ${env.BUILD_TAG} -t ${TicketNumber}  -c '${comment}'""").trim()
        
       // sh 'curl -X POST -H "Content-Type: application/json" http://10.0.1.85:8080/v2/apps -d@msql.json'
        //def comment=sh (returnStdout: true, script: 'curl -X POST -H "Content-Type: application/json" http://10.0.1.85:8080/v2/apps -d@marathon.json' )
        //def result = sh(returnStdout:true , script: """python Integration.py --action Update -b ${env.BUILD_TAG} -t ${TicketNumber}  -c '${comment}'""").trim()
        
        marathon(
        url: 'http://172.29.133.15:8080',
        forceUpdate: true,
        filename: 'dockermarathon.json',
        appId: 'blog',
        docker: "vishaldenge/php10:${gitCommit()}".toString()
        )
        comment="(DEPLOY) Deploying the container stage is completed"
        result = sh(returnStdout:true , script: """python Integration.py --action Update -b ${env.BUILD_TAG} -t ${TicketNumber}  -c '${comment}'""").trim()
   
    stage 'Collect test reports'
        sh 'touch reports/*.xml'
        //
        junit '**/reports/*.xml'
        // step([$class: 'JUnitResultArchiver', testResults: '**/reports/*.xml'])
        
        comment="Collect test reports stage is completed"
        result = sh(returnStdout:true , script: """python Integration.py --action Update -b ${env.BUILD_TAG} -t ${TicketNumber}  -c '${comment}'""").trim()
    
    stage 'Clean up'
        comment="Clean up stage is completed"
        result = sh(returnStdout:true , script: """python Integration.py --action Update -b ${env.BUILD_TAG} -t ${TicketNumber}  -c '${comment}'""").trim()
       

}
