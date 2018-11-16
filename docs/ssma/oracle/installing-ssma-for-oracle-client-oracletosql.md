---
title: Instalación de SSMA para el cliente de Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Licensing SSMA
ms.assetid: d5d4903d-e296-4bbf-8780-63674c4d62d5
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 27e5c0ef0c834806351bda73eb69dbe783d78db2
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51666824"
---
# <a name="installing-ssma-for-oracle-client-oracletosql"></a>Instalación de SSMA para el cliente de Oracle (OracleToSQL)
El cliente SSMA consta de los archivos de programa que realizan las siguientes tareas:  
  
-   Conéctese a una base de datos de Oracle.  
  
-   Conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Convertir los objetos de base de datos de Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxis.  
  
-   Cargar los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Este tema proporciona los requisitos previos de instalación e instrucciones para la instalación de SSMA.  
  
## <a name="prerequisites"></a>Requisitos previos  
SSMA está diseñado para trabajar con Oracle 9 o versiones posteriores y todas las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Antes de instalar SSMA, asegúrese de que el equipo cumple los requisitos siguientes:  
  
-   Windows 7 o versiones posteriores, o Windows Server 2008 o versiones posteriores.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 o una versión posterior.  
  
-   El [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versión 4.0 o una versión posterior. El [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] está disponible en la versión 4.0 del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] medio del producto. También puede obtener desde el [Centro para desarrolladores de .NET Framework](https://go.microsoft.com/fwlink/?LinkId=48882).  
  
-   Cliente Oracle 9.0 o una versión posterior y conectividad a las bases de datos de Oracle que se van a migrar. La versión de cliente de Oracle debe ser la misma versión que, o una versión posterior a la versión de la base de datos de Oracle.  
  
    Puede instalar al cliente de Oracle desde el CD del producto Oracle o desde el sitio Web de Oracle. Para obtener información acerca de la conectividad, consulte [conectarse a Oracle Database &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md).  
  
-   Acceso a y los permisos necesarios en el equipo que hospeda la instancia de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB donde va a migrar datos y objetos de base de datos. Para obtener más información, consulte [conectarse a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md).  
  
-   4 GB de RAM recomendado.  
  
## <a name="installing-the-ssma-for-oracle-client"></a>Instalación de SSMA para el cliente de Oracle  
SSMA es una descarga Web. Para descargar la versión más reciente, consulte el [página de descarga de SQL Server Migration Assistant](https://aka.ms/ssmafororacle).  
  
Después de descargar la versión más reciente, debe extraer los archivos de instalación desde antes de poder instalar SSMA.  
  
**Para instalar al cliente SSMA**  
  
1.  Haga doble clic en SSMA para Oracle *n*. Install.exe, donde *n* es el número de compilación.  
  
2.  En la página de bienvenida, haga clic en **siguiente**.  
  
    Si no tiene instalados los requisitos previos, aparecerá un mensaje que indica que primero debe instalar los componentes necesarios. Asegúrese de que ha instalado todos los requisitos previos y, a continuación, ejecute el programa de instalación de nuevo.  
  
3.  Lea el contrato de licencia de usuario final. Si está de acuerdo, seleccione **acepto los términos del contrato de licencia**y, a continuación, haga clic en **siguiente**.  
  
4.  En la página Elegir tipo de instalación, haga clic en **típica**.  
  
5.  Haga clic en **Instalar**.  
  
> [!IMPORTANT]  
> 1.  Desinstale todas las versiones anteriores de SSMA para Oracle antes de instalar la nueva versión.  
  
La ubicación de instalación predeterminada es C:\Program Files\Microsoft SQL Server Migration Assistant para Oracle.  
  
Además de los archivos de programa SSMA, también debe instalar SSMA para el paquete de extensiones de Oracle en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, consulte [instalación de componentes de SSMA en SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md).  
  
## <a name="see-also"></a>Vea también  
[Instalación de componentes de SSMA en SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[Bases de datos de migración de Oracle a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
