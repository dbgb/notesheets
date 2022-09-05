# Version Control Strategies

## Simple

| Branch merging strategy                  | Deployment environment | Tag |
| ---------------------------------------- | ---------------------- | --- |
| dev -> master                            | stage -> prod          | ?   |
| master -> hotfix/\<fix\> -> dev & master | stage -> prod          | y   |

## Flow

| Branch merging strategy                    | Deployment environment | Tag |
| ------------------------------------------ | ---------------------- | --- |
| dev -> feature/\<feat\> (-> dev)           | test OR (local only)   | n   |
| dev -> release/\<version\> -> dev & master | stage -> prod          | y   |
| master -> hotfix/\<fix\> -> dev & master   | stage -> prod          | y   |
