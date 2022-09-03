# nginx server with certbot client for ssl key management

## Getting started
At first startup nginx will need default ssl keys in order to complete startup to server the acme challenges. For this follow bellow steps

[Reference Article](https://pentacent.medium.com/nginx-and-lets-encrypt-with-docker-in-less-than-5-minutes-b4b8a60d3a71)

1. Create temporary directories to store the keys
```
docker compose run --rm --entrypoint "mkdir -p /etc/letsencrypt/live/bi-frost.xyz/" certbot
```
2. Generate temporary keys
```
docker compose run --rm --entrypoint "openssl req -x509 -nodes -newkey rsa:4096 -days 1 -keyout '/etc/letsencrypt/live/bi-frost.xyz/privkey.pem' -out '/etc/letsencrypt/live/bi-frost.xyz/fullchain.pem' -subj '/CN=localhost'" certbot

docker compose run --rm --entrypoint "cp /etc/letsencrypt/live/bi-frost.xyz/fullchain.pem /etc/letsencrypt/live/bi-frost.xyz/chain.pem" certbot
```
3. Restart Nging service/container
4. Remove temp keys to generate the actual keys
```
docker compose run --rm --entrypoint "rm -rf /etc/letsencrypt/live/bi-frost.xyz" certbot
```
5. Request keys for required domains
```
docker compose run --rm --entrypoint "certbot certonly --webroot -w /var/www/certbot --email admin@bi-frost.xyz -d bi-frost.xyz,www.bi-frost.xyz,portainer.bi-frost.xyz,luthor.bi-frost.xyz,stats.luthor.bi-frost.xyz,pihole.bi-frost.xyz --agree-tos --force-renewal" certbot
```

## Name
Choose a self-explaining name for your project.

## Description
Let people know what your project can do specifically. Provide context and add a link to any reference visitors might be unfamiliar with. A list of Features or a Background subsection can also be added here. If there are alternatives to your project, this is a good place to list differentiating factors.

## Badges
On some READMEs, you may see small images that convey metadata, such as whether or not all the tests are passing for the project. You can use Shields to add some to your README. Many services also have instructions for adding a badge.

## Visuals
Depending on what you are making, it can be a good idea to include screenshots or even a video (you'll frequently see GIFs rather than actual videos). Tools like ttygif can help, but check out Asciinema for a more sophisticated method.

## Installation
Within a particular ecosystem, there may be a common way of installing things, such as using Yarn, NuGet, or Homebrew. However, consider the possibility that whoever is reading your README is a novice and would like more guidance. Listing specific steps helps remove ambiguity and gets people to using your project as quickly as possible. If it only runs in a specific context like a particular programming language version or operating system or has dependencies that have to be installed manually, also add a Requirements subsection.

## Usage
Use examples liberally, and show the expected output if you can. It's helpful to have inline the smallest example of usage that you can demonstrate, while providing links to more sophisticated examples if they are too long to reasonably include in the README.

## Support
Tell people where they can go to for help. It can be any combination of an issue tracker, a chat room, an email address, etc.

## Roadmap
If you have ideas for releases in the future, it is a good idea to list them in the README.

## Contributing
State if you are open to contributions and what your requirements are for accepting them.

For people who want to make changes to your project, it's helpful to have some documentation on how to get started. Perhaps there is a script that they should run or some environment variables that they need to set. Make these steps explicit. These instructions could also be useful to your future self.

You can also document commands to lint the code or run tests. These steps help to ensure high code quality and reduce the likelihood that the changes inadvertently break something. Having instructions for running tests is especially helpful if it requires external setup, such as starting a Selenium server for testing in a browser.

## Authors and acknowledgment
Show your appreciation to those who have contributed to the project.

## License
For open source projects, say how it is licensed.

## Project status
If you have run out of energy or time for your project, put a note at the top of the README saying that development has slowed down or stopped completely. Someone may choose to fork your project or volunteer to step in as a maintainer or owner, allowing your project to keep going. You can also make an explicit request for maintainers.
