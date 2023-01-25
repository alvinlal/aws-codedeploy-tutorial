# Role trust policy 

`json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Federated": "arn:aws:iam::732313143489:oidc-provider/token.actions.githubusercontent.com"
            },
            "Action": "sts:AssumeRoleWithWebIdentity",
            "Condition": {
                "StringEquals": {
                    "token.actions.githubusercontent.com:aud": "sts.amazonaws.com"
                },
                "StringLike": {
                    "token.actions.githubusercontent.com:sub": "repo:alvinlal/codedeploy-tutorial:ref:refs/heads/master"
                }
            }
        }
    ]
}
`

# Policy for github actions

`json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "codedeploy:CreateDeployment",
                "codedeploy:GetDeploymentConfig",
                "codedeploy:RegisterApplicationRevision"
            ],
            "Resource": [
                "arn:aws:codedeploy:ap-south-1:732313143489:deploymentgroup:codedeploy-tutorial/codedeploy-deployment-group",
                "arn:aws:codedeploy:ap-south-1:732313143489:application:codedeploy-tutorial",
                "arn:aws:codedeploy:ap-south-1:732313143489:deploymentconfig:CodeDeployDefault.OneAtATime"
            ]
        }
    ]
}
`