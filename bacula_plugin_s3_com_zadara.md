# Repositório de Configurações do Bacula

### Configuração do plugin S3 para Zadara

Adicionadr ao bacula-sd.conf

```
Cloud {
  Name = "CloudZadara"
  Driver = "S3"
  # Obter no painel do Zadara as configurações a seguir
  Hostname = ""
  Region = ""
  AccessKey = ""
  SecretKey = ""
  Bucketname = ""
  Protocol = "HTTPS"
  UriStyle = "Path"
  TruncateCache = "AfterUpload"
  Upload = "EachPart"
  MaximumConcurrentUploads = "20"
  MaximumConcurrentDownloads = "20"
}

Autochanger {
  Name = DeviceZadaraChgr1
  Device = DeviceZadara-Dev1, DeviceZadara-Dev2
  Changer Command = ""
  Changer Device = /dev/null
}


Device {
  Name = "DeviceZadara-Dev1"
  MediaType = "MediaZadara"
  DeviceType = "Cloud"
  ArchiveDevice = "/mnt/cache"
  RemovableMedia = no
  RandomAccess = yes
  AutomaticMount = yes
  LabelMedia = yes
  AlwaysOpen = no
  MaximumPartSize = 1 GB
  Cloud = "CloudZadara"
}

Device {
  Name = "DeviceZadara-Dev2"
  MediaType = "MediaZadara"
  DeviceType = "Cloud"
  ArchiveDevice = "/mnt/cache"
  RemovableMedia = no
  RandomAccess = yes
  AutomaticMount = yes
  LabelMedia = yes
  AlwaysOpen = no
  MaximumPartSize = 1 GB
  Cloud = "CloudZadara"
}
```

Adicionar ao bacula-dir.conf

```
Autochanger {
  Name = MediaZadara
  Address = "" # adicionar ip do servidor
  SDPort = 9103
  Password = "" # Configurar senha
  Device = DeviceZadaraChgr1
  Media Type = MediaZadara
  Maximum Concurrent Jobs = 2         # run up to 10 jobs a the same time
  Autochanger = MediaZadara                 # point to ourself
}
```
