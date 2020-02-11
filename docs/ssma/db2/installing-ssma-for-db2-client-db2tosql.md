---
title: Instalación de SSMA para el cliente DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 09/07/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 3ae2a470-6afd-4512-b6d1-fcbe6afe88ad
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 1623430eed752db7fa387caf33124082eb318490
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "70774184"
---
# <a name="installing-ssma-for-db2-client-db2tosql"></a>Instalación de SSMA para el cliente DB2 (DB2ToSQL)

El cliente de SSMA está formado por los archivos de programa que realizan las siguientes tareas:  
  
- Conéctese a una base de datos DB2.  
  
- Conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
- Convierte los objetos de base [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de datos DB2 en sintaxis.  
  
- Cargue los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
- Migre los datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
En este tema se proporcionan los requisitos previos de instalación y las instrucciones para instalar SSMA.  
  
## <a name="prerequisites"></a>Prerequisites

SSMA está diseñado para funcionar con DB2 en la versión 9,0 de z/OS y 10,0 o DB2 en la versión 9,8 de LUW y 10,1 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o versiones posteriores 2012, o en versiones posteriores.  
  
Antes de instalar SSMA, asegúrese de que el equipo cumple los requisitos siguientes:  
  
- Windows 7 o versiones posteriores, o Windows Server 2008 o versiones posteriores.  
  
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3,1 o versiones posteriores.  
  
- La [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versión 4,0 o una versión posterior. La [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versión 4,0 está disponible en los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] medios del producto. También puede obtenerlo en el [Centro para desarrolladores de .NET Framework](https://go.microsoft.com/fwlink/?LinkId=48882).  
  
- Proveedor OLEDB de Microsoft para DB2 versión 5 o una versión posterior, y conectividad con las bases de datos DB2 que desea migrar.  
  
- Acceso y permisos suficientes en el equipo que hospeda la instancia de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL dB, donde se van a migrar los datos y los objetos de base de datos. Para obtener más información, vea [conectarse a SQL Server &#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md).  
  
- se recomiendan 4 GB de RAM.  
  
## <a name="microsoft-oledb-provider-for-db2"></a>Proveedor Microsoft OLE DB para DB2  

Para descargar el proveedor OLEDB para DB2 versión 6,0, vaya a [Microsoft® SQL Server® 2017 Feature Pack](https://www.microsoft.com/download/details.aspx?id=55992).

SSMA es una descarga Web. Para descargar la versión más reciente, consulte la [Página de descarga de SQL Server Migration Assistant](https://aka.ms/ssmafordb2).  
  
Después de descargar la versión más reciente, extraiga los archivos de instalación para poder instalar SSMA.  
  
Para instalar el cliente de SSMA:
  
1. Haga doble clic en SSMA para DB2 *n*. Instale. exe, donde *n* es el número de compilación.  
  
2. En la página **principal**, seleccione **Siguiente**.  
  
   Si no tiene instalados los requisitos previos, aparecerá un mensaje que indica que primero debe instalar los componentes necesarios. Asegúrese de que ha instalado todos los requisitos previos y, a continuación, vuelva a ejecutar el programa de instalación.  
  
3. Lea el contrato de licencia para el usuario final. Si está de acuerdo, seleccione Acepto **los términos del contrato de licencia**y, después, seleccione **siguiente**.  
  
4. En la página **elegir tipo de instalación** , seleccione **típica**.  
  
5. Seleccione **Instalar**.  
  
> [!IMPORTANT]  
> Desinstale todas las versiones anteriores de SSMA para DB2 antes de instalar la nueva versión.
  
La ubicación de instalación predeterminada es C:\Archivos de Programa\microsoft SQL Server Migration Assistant para DB2.  
  
## <a name="see-also"></a>Consulte también

[Instalación de componentes de SSMA en SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
[Migrar bases de datos DB2 a SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
