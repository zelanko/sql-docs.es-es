---
title: Actualizar el esquema de las bases de datos DQS después de instalar la actualización de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: c8f3fbae-02c4-464d-a35c-7108f48c58cb
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e4d4f5af2a9b0c58e8cef89f143e4ec42cb03695
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53372927"
---
# <a name="upgrade-dqs-databases-schema-after-installing-sql-server-update"></a>Actualizar el esquema de las bases de datos DQS tras instalar la actualización de SQL Server
  Tras instalar una actualización de SQL Server (revisión o actualización acumulativa) en una instancia de DQS configurada previamente, puede que tenga que actualizar el esquema de bases de datos DQS ejecutando el archivo DQSInstaller.exe con el parámetro de la línea de comandos **upgrade** . De lo contrario, podría recibir un mensaje de error similar al siguiente al intentar conectarse a Data Quality Server con su Data Quality Client:  
  
```  
An error occurred in the Microsoft .NET Framework while trying to load assembly id 65581.  
```  
  
 La actualización del esquema de bases de datos DQS no afecta a los datos actuales de las bases de datos DQS (bases de conocimiento, proyectos de calidad de datos y resultados exportados en la base de datos DQS_STAGING_DATA). Sin embargo, debe hacer una copia de seguridad de las bases de datos DQS antes de actualizar el esquema de las bases de datos DQS para impedir la pérdida accidental de datos durante la actualización del esquema. Para obtener información sobre la copia de seguridad de bases de datos de DQS, vea [Backing Up and Restoring DQS Databases](../backing-up-and-restoring-dqs-databases.md).  
  
> [!NOTE]  
>  La mayor parte de las actualizaciones de SQL Server requerirán una actualización del esquema de bases de datos DQS. Para obtener información acerca de las actualizaciones de SQL Server que requerirán una actualización en el esquema de bases de datos DQS, vea el gráfico del paso 1.A en [actualizar DQS: Instalar actualizaciones acumulativas o revisiones en Data Quality Services](https://go.microsoft.com/fwlink/?LinkID=251565).  
  
## <a name="prerequisites"></a>Requisitos previos  
  
-   Debe haber iniciado sesión como miembro del grupo Administradores en el equipo con [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] .  
  
-   La cuenta de usuario de Windows debe ser miembro del rol fijo de servidor sysadmin en la instancia de SQL Server donde está instalado [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] .  
  
### <a name="to-upgrade-dqs-databases-schema"></a>Para actualizar el esquema de bases de datos DQS  
  
1.  (Recomendado) Haga copia de seguridad de sus bases de datos DQS antes de continuar con la actualización del esquema. Para obtener información sobre la copia de seguridad de bases de datos de DQS, vea [Backing Up and Restoring DQS Databases](../backing-up-and-restoring-dqs-databases.md).  
  
2.  Inicie el símbolo del sistema.  
  
3.  En el símbolo del sistema, cambie el directorio a la ubicación donde DQSInstaller.exe esté disponible. Si instaló la instancia predeterminada de SQL Server, el archivo DQSInstaller.exe estará disponible en C:\Archivos de programa\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn:  
  
    ```  
    cd C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn  
    ```  
  
4.  En el símbolo del sistema, escriba el siguiente comando y presione ENTRAR:  
  
    ```  
    dqsinstaller.exe -upgrade  
    ```  
  
5.  El instalador le pregunta si desea realizar la copia de seguridad de las bases de datos DQS antes de continuar. Si aún no la ha hecho, escriba `Y` o `Yes` y presione ENTRAR para continuar con la actualización.  
  
6.  Se muestra un mensaje para indicar que la actualización del esquema de las bases de datos DQS se realizó.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Inicie sesión en el servidor Data Quality Server actualizado desde una aplicación Data Quality Client.  
  
 Para obtener más información acerca de cómo actualizar DQS actualiza el esquema de bases de datos después de instalar SQL Server y los pasos de solución de problemas asociados, consulte [actualizar DQS: Instalar actualizaciones acumulativas o revisiones en Data Quality Services](https://go.microsoft.com/fwlink/?LinkID=251565).  
  
## <a name="see-also"></a>Vea también  
 [Instalar Data Quality Services](install-data-quality-services.md)   
 [Actualizar ensamblados de SQLCLR después de actualizar .NET Framework](upgrade-sqlclr-assemblies-after-net-framework-update.md)  
  
  
