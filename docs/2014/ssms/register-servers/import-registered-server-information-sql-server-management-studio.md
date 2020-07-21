---
title: Importar información de servidores registrados
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.importregisteredservers.f1
helpviewer_keywords:
- transferring registered server information
- Registered Servers [SQL Server], importing
- importing registered server information
ms.assetid: cc497a14-1360-4887-b70c-002f042823b6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ddf4a72fa81e12f49b8974881dd964473c863c28
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85048705"
---
# <a name="import-registered-server-information-sql-server-management-studio"></a>Importar información de servidores registrados (SQL Server Management Studio)
  En este tema se describe cómo importar información guardada de servidores registrados en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. La exportación e importación de archivos de un servidor registrado permite configurar fácilmente varios equipos con los mismos servidores en Servidores registrados. Esto resulta útil cuando se administra un gran número de servidores desde equipos en distintas ubicaciones, o cuando desea establecer la configuración de conexión básica para un usuario menos experimentado.  
  
> [!NOTE]  
>  No puede importar información de servidores registrados en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] desde versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-import-registered-server-information"></a>Para importar información de servidores registrados  
  
1.  En Servidores registrados, haga clic en el tipo de servidor en la barra de herramientas Servidores registrados. El tipo de servidor debe ser el mismo que el tipo de archivo de exportación de servidores registrados. Por ejemplo, si ha exportado la información de un servidor registrado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe hacer clic en **SQL Server** en la barra de herramientas Servidores registrados.  
  
2.  Haga clic con el botón derecho en un grupo de servidores y seleccione **Importar**.  
  
3.  En el cuadro de diálogo **Importar servidores registrados** , seleccione el archivo de servidores registrados que desea importar y, a continuación, haga clic en **Aceptar**.  
  
     **Importar archivo**  
     Escriba el nombre del archivo de importación en el cuadro de texto o haga clic en el botón Explorar ( **...** ) para localizar el archivo en el equipo cliente. Si selecciona un archivo existente, la información del servidor registrado se anexa al archivo. El archivo de importación solo puede ser un archivo de servidor registrado exportado previamente. Los archivos de servidor registrado tienen una extensión .regsrvr.  
  
     **Seleccionar el grupo de servidores de destino de la importación**  
     Seleccione el nodo raíz o un grupo de servidores específico al que se importarán las entradas del servidor registrado del archivo. Puede importar al archivo de exportación todos los servidores registrados, los servidores registrados de un grupo de servidores específico o un único servidor registrado. La funcionalidad de importación es recursiva; por ejemplo, si un grupo de servidores A contiene un grupo de servidores B, y un grupo de servidores B contiene grupos de servidores C y D; la importación del grupo de servidores A exporta todas las entradas de A, B, C y D.  
  
     El grupo de servidores muestra solo los grupos del actual árbol de servidores registrados.  
  
     Si selecciona un grupo de servidores o un servidor para la importación, un mensaje confirmará que desea sobrescribir el grupo de servidores o el servidor existente.  
  
 Los registros de servidor que usan la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] almacenan las contraseñas por usuario. Después de importar los registros de servidor, los usuarios deben escribir la contraseña para cada servidor la primera vez que se conectan, y almacenar así las contraseñas en las listas de los servidores registrados. Esto no es necesario en los servidores registrados mediante la autenticación de Windows.  
  
## <a name="see-also"></a>Consulte también  
 [Cambiar el registro de un servidor &#40;SQL Server Management Studio&#41;](change-a-server-s-registration-sql-server-management-studio.md) [exportar información de servidores registrados &#40;SQL Server Management Studio](export-registered-server-information-sql-server-management-studio.md)&#41;   
 [Crear un servidor registrado &#40;SQL Server Management Studio&#41;](create-a-new-registered-server-sql-server-management-studio.md)  
  
  
