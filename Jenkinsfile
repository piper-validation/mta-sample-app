

node(){
  stage('Prepare')   {
      deleteDir()
      checkout scm
      setupCommonPipelineEnvironment script:this
  }

  stage('Build')   {
      mtaBuild script:this
  }

  stage('Deploy')   {
      def id = new Date().getTime()
      consumerTestCfSpaceName = "val-it-${id}"

      cloudFoundryCreateSpace script: this, cfSpace: consumerTestCfSpaceName
      cloudFoundryDeploy script:this,
                         deployTool: 'mtaDeployPlugin',
                         cloudFoundry:[ space: consumerTestCfSpaceName]
      cloudFoundryDeleteSpace script: this, cfSpace: consumerTestCfSpaceName
  }
}

