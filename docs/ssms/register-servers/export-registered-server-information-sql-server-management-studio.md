---
title: "Exportar información de servidores registrados (SQL Server Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.exportregisteredservers.f1
helpviewer_keywords:
- Registered Servers [SQL Server], exporting
- exporting registered server information
- transferring registered server information
ms.assetid: b65e168f-b6bf-489c-b8ad-3b8644acf0b6
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 5db067d5a2fe5bbf9953484c9a999ed7b1fcddae
ms.openlocfilehash: 384095b7fc904f9e8d57cb3d71a1bd074900c86a
ms.contentlocale: es-es
ms.lasthandoff: 07/31/2017

---
# <a name="export-registered-server-information-sql-server-management-studio"></a>Exportar información de servidores registrados (SQL Server Management Studio)
  En este tema se describe cómo guardar y exportar información de servidores registrados en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]para distribuirla a otros empleados o servidores. Puede utilizar esta característica de exportación para crear una interfaz de usuario coherente en varios equipos.  
  
 La exportación y posterior importación de archivos de servidores registrados permite configurar fácilmente varios equipos con los mismos servidores en Servidores registrados. Esto resulta útil cuando se administra un gran número de servidores desde equipos en varias ubicaciones, o cuando se desea configurar un usuario menos experto con una configuración de conexión básica.  
  
> [!NOTE]  
>  Los registros de servidor que usan la autenticación de SQL Server almacenan las contraseñas por usuario. Después de exportar e importar los registros de servidor, los usuarios deben escribir la contraseña para cada servidor la primera vez que se conectan, y almacenar así las contraseñas en las listas de los servidores registrados. Esto no es necesario en los servidores registrados mediante la autenticación de Windows.  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-export-registered-server-information"></a>Para exportar información del servidor registrado  
  
1.  En Servidores registrados, haga clic con el botón derecho en un grupo de servidores y, luego, haga clic en **Exportar**.  
  
    > [!NOTE]  
    >  Se puede exportar un solo servidor, todo el árbol de servidores registrados o un subconjunto del árbol.  
  
2.  En el cuadro de diálogo **Exportar servidores registrados** , realice las selecciones siguientes.  
  
     **Grupo del servidor**  
     Especifique el grupo de servidores que se va a exportar. Puede exportar todos los servidores registrados, los servidores registrados de un grupo de servidores determinado o un solo servidor registrado. La función de exportación es recursiva; por ejemplo, si el grupo de servidores A contiene el grupo de servidores B y éste contiene los grupos C y D, la exportación del grupo A exporta todas las entradas de A, B, C y D.  
  
     El grupo de servidores muestra solo los grupos del actual árbol de servidores registrados.  
  
     **Archivo de exportación**  
     Escriba el nombre del archivo de exportación en el cuadro de texto o use el botón Examinar (**...**) para buscar un archivo de exportación en el equipo cliente. Si selecciona un archivo existente, la información del servidor registrado se anexa al archivo. Utilice la extensión .regsrvr. Si desea que la información del servidor registrado esté disponible para otros usuarios u otro equipo, puede guardar el archivo en la red. De este modo, otros usuarios podrán obtener acceso al archivo e importar parte o la totalidad de la información del servidor registrado. Si selecciona un archivo existente como archivo de exportación, el contenido del archivo se sobrescribirá con la información del servidor registrado.  
  
     **No incluir nombres de usuario ni contraseñas en el archivo de exportación**  
     Excluye los nombres de usuario en la exportación del archivo.  
  
    > [!IMPORTANT]  
    >  Los archivos de exportación están cifrados; sin embargo, si se incluyen nombres de usuario y contraseñas para la autenticación de SQL Server, el acceso al archivo debe controlarse cuidadosamente. De manera predeterminada, los nombres de usuario y las contraseñas se excluyen del archivo de exportación.  
  
## <a name="see-also"></a>Vea también  
 [Importar información de servidores registrados &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/import-registered-server-information-sql-server-management-studio.md)   
 [Crear un servidor registrado &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-a-new-registered-server-sql-server-management-studio.md)  
  
  
