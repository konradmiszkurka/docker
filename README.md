# docker
1. docker-compose up
2. docker exec -it docker_phpfpm_1 bash
3. cd /code
4. composer install
5. exit
5. mv docker/.env.example ../backend/.env.local
6. docker exec -it docker_phpfpm_1 bash
7. cd /code
8. php bin/console doctrine:migrations:migrate
9. php bin/console doctrine:fixtures:load --append
10. php vendor/bin/codecept run  <- to run tests