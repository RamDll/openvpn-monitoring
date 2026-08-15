# openvpn-monitoring

Стек мониторинга для [ovpn-admin-hardened](https://github.com/RamDll/ovpn-admin-hardened) — Prometheus + Grafana + node-exporter.

## Что собирается

- **ovpn-admin** метрики: подключённые клиенты, трафик по клиентам, срок годности сертификатов (`http://openvpn:8080/metrics`)
- **node-exporter**: CPU, RAM, диск, аптайм сервера

Хранение метрик — 365 дней (`--storage.tsdb.retention.time=365d` в `prometheus.yml`).

## Требования

- Уже запущенный стек [ovpn-admin-hardened](https://github.com/RamDll/ovpn-admin-hardened) — используется его docker-сеть (`openvpn-master_default`)

## Быстрый старт

1. Клонировать:
```bash
   git clone git@github.com:RamDll/openvpn-monitoring.git
   cd openvpn-monitoring
```

2. Создать `.env`:
```bash
   cat > .env << 'ENVEOF'
   VPS_PUBLIC_IP=ВАШ_IP
   GRAFANA_ADMIN_PASSWORD=НАДЁЖНЫЙ_ПАРОЛЬ
   ENVEOF
```

3. Запустить:
```bash
   docker compose up -d
```

Grafana доступна на `127.0.0.1:3000` — снаружи рекомендуется проксировать через nginx с TLS, как и панель ovpn-admin.
