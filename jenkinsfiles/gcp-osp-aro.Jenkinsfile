podTemplate(yaml: readTrusted('jenkinsfiles/SubmarinerAgentPod.yaml')) {
    node(POD_LABEL) {
        checkout scm

        properties([
            parameters([
                booleanParam(name: 'GLOBALNET', defaultValue: true, description: 'Deploy Globalnet on Submariner'),
                booleanParam(name: 'DOWNSTREAM', defaultValue: true, description: 'Deploy downstream version of Submariner'),
                extendedChoice(name: 'JOB_STAGES', description: 'Select the stages of the job to be executed',
                    value: 'Deploy OCP cluster,Deploy ACM Hub,Deploy Clusters by ACM,Deploy Managed OCP,Import OCP into ACM Hub,Submariner Validate prerequisites,Submariner Deploy,Submariner Test - E2E,Submariner Test - Cypress UI,Report to Polarion',
                    defaultValue: 'Deploy OCP cluster,Deploy ACM Hub,Deploy Clusters by ACM,Deploy Managed OCP,Import OCP into ACM Hub,Submariner Validate prerequisites,Submariner Deploy,Submariner Test - E2E,Submariner Test - Cypress UI,Report to Polarion',
                    multiSelectDelimiter: ',', type: 'PT_CHECKBOX', visibleItemCount: 10),
                credentials(name: 'SUBMARINER_CONFIG', defaultValue: 'acm-2.9-subm-0.16-gcp-osp-aro', description: 'Submariner config for environment deploy',
                    required: true, credentialType: 'org.jenkinsci.plugins.plaincredentials.impl.FileCredentialsImpl'),
                string(name: 'NODE_TO_LABEL_AS_GW', defaultValue: 'mbabushk-osp', description: 'Specify cluster node to be manually labeled as Submariner Gateway')
            ])
        ])

        container('submariner') {
            load 'jenkinsfiles/base.Jenkinsfile'
        }
    }
}