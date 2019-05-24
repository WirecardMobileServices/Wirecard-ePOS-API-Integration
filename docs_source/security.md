## Get info about current user
    
    GET https://switch.wirecard.com/mswitch-server/v1/security/currentUser

## Get password policy
    
    GET https://switch.wirecard.com/mswitch-server/v1/security/passwordPolicy
        
## Manage user credentials

### Change password

    POST https://switch.wirecard.com/mswitch-server/v1/security/credentials?action=changePassword
    
        {
            "currentPassword": "{{UserCurrentPassword}}",
            "newPassword": "{{UserNewPassword}}"
        }
        
### Request password reset

    POST https://switch.wirecard.com/mswitch-server/v1/security/credentials?action=requestPasswordReset
    
        {
            "password": "string",
            "token": "string"
        }