# Smart Home
В данном файле собран джентльменский набор софта для организации умного дома, а также дополнительные программы, который призваны сделать обетание в доме более комфортным и приятным.


## Torrent + OpenVPN

Для получения возможности анонимного пользования торрентом необходимо создать несколько небольшой Docker Compoer файл и добавить конфигурацию для обеих сервисов.

***docker-compose.yaml***

    version: '3.3
    services:
      transmission-openvpn:
        restart: always
        cap_add:
          - NET_ADMIN
        image: haugene/transmission-openvpn
        env_file: ./.env
        volumes:
          - ./data:/data
          - ./config:/config
        logging:
          driver: json-file
          options:
            max-size: 10m
        ports:
          - 9091:9091
***.env***

    OPENVPN_USERNAME=<user>
    OPENVPN_PASSWORD=<pass>
    OPENVPN_PROVIDER=PIA
    OPENVPN_CONFIG=poland
    LOCAL_NETWORK=192.168.0.0/24
    TRANSMISSION_RPC_AUTHENTICATION_REQUIRED=true
    TRANSMISSION_RPC_USERNAME=<user>
    TRANSMISSION_RPC_PASSWORD=<pass>

> Не забудь изменить IP согласно настройкам своей локальной сети, иначе доступа к UI не будет. Данный IP соответствует локальной сети с диапазоном адресов 192.168.0.1-254 и маске 255.255.255.0

