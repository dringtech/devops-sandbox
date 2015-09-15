

FATAL: role "gitlab" does not exist

#Login to PostgreSQL
# Create a user for GitLab
psql -h gitlabdb -U postgres -d template1 -c "CREATE USER gitlab CREATEDB;"
/opt/gitlab/bin/gitlab-rake db:create db:migrate
