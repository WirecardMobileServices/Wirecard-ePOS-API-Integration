This chapter describes calls related to security.

## Get info about current user
    
    GET https://switch.wirecard.com/mswitch-server/v1/security/currentUser

## Get password policy
    
    GET https://switch.wirecard.com/mswitch-server/v1/security/passwordPolicy
        
## Manage user credentials

### Change password

    POST https://switch.wirecard.com/mswitch-server/v1/security/credentials?action=changePassword
    
        {
            "currentPassword": "{currentPassword}",
            "newPassword": "{newPassword}"
        }
        
### Request password reset

    POST https://switch.wirecard.com/mswitch-server/v1/security/credentials?action=requestPasswordReset
    
        {
            "username": "{username}"
        }