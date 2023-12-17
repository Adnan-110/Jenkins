node{
    stage('Test'){
        print "Hello World"
        sh(script:"env")
    }
    if(env.TAG_NAME != "" || env.TAG_NAME != null){
        stage('Executing on Tag Name'){
            print "Executed on Tag"
        }
    }
    else{
        stage('Executing on Branch') {
            print "Executed on Branch"
        }
    }
}