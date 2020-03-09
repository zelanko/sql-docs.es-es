---
title: Compatibilidad de SqlClient con LocalDB
description: Describe la compatibilidad de SqlClient con las bases de datos de LocalDB.
ms.date: 08/15/2019
ms.assetid: cf796898-5575-46f2-ae6e-21e5aa8c4123
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 9a7f5f4a806905f2eea3ce6f8e0c723fdef2347a
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896316"
---
# <a name="sqlclient-support-for-localdb"></a>Compatibilidad de SqlClient con LocalDB

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

A partir del nombre de código de SQL Server Denali, estará disponible una versión ligera de SQL Server, denominada LocalDB. En este tema se describe cómo conectarse a una base de datos de LocalDB.  
  
## <a name="remarks"></a>Observaciones  
Para obtener más información sobre LocalDB, incluido cómo instalar y configurar la instancia de LocalDB, vea los Libros en pantalla de SQL Server.  
  
Para resumir lo que puede hacer con LocalDB:  
  
- Crear e iniciar instancias de LocalDB con sqllocaldb. exe o el archivo app.config.  
  
- Use sqlcmd.exe para agregar y modificar bases de datos en una instancia de LocalDB. Por ejemplo, `sqlcmd -S (localdb)\myinst`.  
  
- Utilice la palabra clave de cadena de conexión `AttachDBFilename` para agregar una base de datos a la instancia de LocalDB. Al usar `AttachDBFilename`, si no especifica el nombre de la base de datos con la palabra clave de la cadena de conexión `Database`, la base de datos se quita de la instancia de LocalDB cuando se cierra la aplicación.  
  
- Especifique una instancia de LocalDB en la cadena de conexión. Por ejemplo, el nombre de instancia es `myInstance`, la cadena de conexión incluiría:  
  
```console
server=(localdb)\\myInstance  
```  
  
`User Instance=True` no se permite al conectarse a una base de datos de LocalDB.  
  
Puede descargar LocalDB desde [Microsoft SQL Server 2012 Feature Pack](https://www.microsoft.com/download/en/details.aspx?id=29065). Si va a usar sqlcmd.exe para modificar datos en la instancia de LocalDB, necesita sqlcmd de SQL Server 2012, que también puede obtener de SQL Server 2012 Feature Pack.  
  
## <a name="programmatically-create-a-named-instance"></a>Creación de una instancia con nombre mediante programación  
Una aplicación puede crear una instancia con nombre y especificar una base de datos de la siguiente manera:  
  
- Especifique las instancias de LocalDB que se van a crear en el archivo app.config, como se indica a continuación.  El número de versión de la instancia debe ser el mismo que el número de versión de la instalación de LocalDB.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <configSections>  
        <section  
        name="system.data.localdb"  
        type="System.Data.LocalDBConfigurationSection,System.Data,Version=4.0.0.0,Culture=neutral,PublicKeyToken=b77a5c561934e089"/>  
      </configSections>  
      <system.data.localdb>  
        <localdbinstances>  
          <add name="myInstance" version="11.0" />  
        </localdbinstances>  
      </system.data.localdb>  
    </configuration>  
    ```  
  
- Especifique el nombre de la instancia utilizando la palabra clave de cadena de conexión `server`.  El nombre de instancia especificado en la palabra clave de la cadena de conexión `server` debe coincidir con el nombre especificado en el archivo app.config.  
  
- Use la palabra clave de cadena de conexión `AttachDBFilename` para especificar el archivo .MDF.  
  
## <a name="next-steps"></a>Pasos siguientes
- [Características de SQL Server y ADO.NET](sql-server-features-adonet.md)
