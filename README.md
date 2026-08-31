services:
  postgis:
    image: postgis/postgis:16-3.4
    environment:
      POSTGRES_DB: gisdb
      POSTGRES_PASSWORD: postgres
    ports:
      - "5432:5432"
    volumes:
      - pg_data:/var/lib/postgresql/data

  geoserver:
    image: kartoza/geoserver
    depends_on:
      - postgis
    environment:
      GEOSERVER_ADMIN_USER: admin
      GEOSERVER_ADMIN_PASSWORD: geoserver
      # แก้ปัญหา Login ไม่ได้บน Codespaces (Content-Security-Policy บล็อก
      # เพราะ GeoServer ไม่รู้ URL สาธารณะของตัวเอง) — ตัวแปร
      # CODESPACE_NAME และ GITHUB_CODESPACES_PORT_FORWARDING_DOMAIN นี้
      # GitHub Codespaces ตั้งค่าให้อัตโนมัติอยู่แล้วในทุกเครื่อง
      # จึงไม่ต้องแก้ไขค่านี้เองไม่ว่าจะเป็น Codespace ของใคร
      org.geoserver.web.csp.strict: "false"
      HTTP_SCHEME: "https"
      HTTP_PROXY_NAME: ${CODESPACE_NAME}-8080.${GITHUB_CODESPACES_PORT_FORWARDING_DOMAIN}
      HTTP_PROXY_PORT: "443"
    ports:
      - "8080:8080"
    volumes:
      # เก็บ Workspace/Datastore/Layer ไว้ถาวร ไม่หายแม้ container
      # จะถูกสร้างใหม่ (เช่น ตอนแก้ไข docker-compose.yml)
      - gs_data:/opt/geoserver/data_dir

volumes:
  pg_data:
  gs_data:
