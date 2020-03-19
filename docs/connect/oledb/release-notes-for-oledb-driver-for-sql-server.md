---
title: Notas de la versión (OLE DB Driver for SQL Server)
ms.date: 02/27/2020
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: genemi
author: mateusz-kmiecik
ms.author: v-makmie
ms.openlocfilehash: c0a9e1726958a1eda7cf71817479f7c37dcfe854
ms.sourcegitcommit: 4bba3c8e3360bcbe269819d61f8898d0ad52c6e3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/11/2020
ms.locfileid: "79090526"
---
# <a name="release-notes-for-the-microsoft-ole-db-driver-for-sql-server"></a>Notas de la versión del controlador Microsoft OLE DB para SQL Server

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

En esta página se describe lo que se ha agregado en cada versión del controlador Microsoft OLE DB para SQL Server.

<!--
USE THE TABLE FORMAT!
Hello, from now on, please use the table-based format standard for all new Release Notes content.
See section "## 18.2.1" for a live example in this article.
Thank you. For questions, contact GeneMi. (2019/03/16)
-->

## <a name="1830"></a>18.3.0

![descargar](../../ssms/media/download-icon.png) [Descargar instalador x64](https://go.microsoft.com/fwlink/?linkid=2117515)  
![descargar](../../ssms/media/download-icon.png) [Descargar instalador x86](https://go.microsoft.com/fwlink/?linkid=2117517)  

Fecha de publicación: Octubre de 2019

Si necesita descargar el instalador en un idioma distinto al que se ha detectado, puede usar estos vínculos directos.  
Para el controlador x64: [Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x804) | [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x40a)  
Para el controlador x86: [Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x804) | [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x40a)  

### <a name="features-added"></a>Características agregadas

| Característica agregada | Detalles |
| :------------ | :------ |
| Compatibilidad con la autenticación de Azure Active Directory (`ActiveDirectoryInteractive`, `ActiveDirectoryMSI`). | [Uso de Azure Active Directory](features/using-azure-active-directory.md). |
| Incluye la biblioteca de autenticación de Azure Active Directory (ADAL) y el instalador. | Ahora incluido en la instalación del controlador base, el instalador OLE DB actualizará las instalaciones existentes de la Biblioteca de autenticación de Microsoft Active Directory para SQL Server, y las quita de la lista de aplicaciones instaladas en Windows. |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>Errores corregidos

| Error corregido | Detalles |
| :-------- | :------ |
| Se corrigió la lógica de DROP INDEX en [IIndexDefinition::DropIndex](https://go.microsoft.com/fwlink/?linkid=2106448). | Las versiones anteriores del controlador de OLE DB no pueden quitar un índice de clave principal cuando el identificador de esquema y el identificador de usuario del propietario del índice no son iguales. |
| &nbsp; | &nbsp; |

## <a name="previous-releases"></a>Versiones anteriores

Para descargar las versiones anteriores del controlador OLE DB, haga clic en los vínculos de descarga de las secciones siguientes:

## <a name="1823"></a>18.2.3

![descargar](../../ssms/media/download-icon.png) [Descargar instalador x64](https://go.microsoft.com/fwlink/?linkid=2119554)  
![descargar](../../ssms/media/download-icon.png) [Descargar instalador x86](https://go.microsoft.com/fwlink/?linkid=2119738)  

Fecha de publicación: Junio de 2019

Si necesita descargar el instalador en un idioma distinto al que se ha detectado, puede usar estos vínculos directos.  
Para el controlador x64: [Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x804) | [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x40a)  
Para el controlador x86: [Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x804) | [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x40a)  

### <a name="features-added-in-1823"></a>Características agregadas en la versión 18.2.3

| Característica agregada | Detalles |
| :------------ | :------ |
| Compatibilidad con las actualizaciones de controladores desde medios extraíbles de SQL Server. | Esta mejora permite actualizar controladores directamente desde medios extraíbles de SQL Server. |
| &nbsp; | &nbsp; |

## <a name="1822"></a>18.2.2

![descargar](../../ssms/media/download-icon.png) [Descargar instalador x64](https://go.microsoft.com/fwlink/?linkid=2118512)  
![descargar](../../ssms/media/download-icon.png) [Descargar instalador x86](https://go.microsoft.com/fwlink/?linkid=2118415)  

Fecha de publicación: Mayo de 2019

Si necesita descargar el instalador en un idioma distinto al que se ha detectado, puede usar estos vínculos directos.  
Para el controlador x64: [Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x804) | [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x40a)  
Para el controlador x86: [Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x804) | [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x40a)  

### <a name="bugs-fixed-in-1822"></a>Errores corregidos en la versión 18.2.2

| Error corregido | Detalles |
| :-------- | :------ |
| Se ha corregido un problema de interactividad en la autenticación de Azure Active Directory en contenedores multiproceso (MTA). | El controlador OLE DB 18.2.1 intenta cambiar por error el modelo de simultaneidad de COM en un contenedor previamente inicializado como multiproceso (MTA). Como resultado de esto, en una aplicación que realiza más de una llamada subsiguiente a [CoInitialize](https://go.microsoft.com/fwlink/?linkid=2092520) o [CoInitializeEx](https://go.microsoft.com/fwlink/?linkid=2092521) antes de llamar a la interfaz [IDBInitialize::Initialize](https://go.microsoft.com/fwlink/?linkid=2092522), el controlador no puede establecer una conexión al usar cualquier modo de autenticación de Azure Active Directory. |
| &nbsp; | &nbsp; |

## <a name="1821"></a>18.2.1

![descargar](../../ssms/media/download-icon.png) [Descargar instalador x64](https://go.microsoft.com/fwlink/?linkid=2118511)  
![descargar](../../ssms/media/download-icon.png) [Descargar instalador x86](https://go.microsoft.com/fwlink/?linkid=2118278)  

Fecha de publicación: Febrero de 2019

Si necesita descargar el instalador en un idioma distinto al que se ha detectado, puede usar estos vínculos directos.  
Para el controlador x64: [Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x804) | [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x40a)  
Para el controlador x86: [Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x804) | [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x40a)  

### <a name="features-added-in-1821"></a>Características agregadas en la versión 18.2.1

| Característica agregada | Detalles |
| :------------ | :------ |
| Compatibilidad con la codificación de servidor UTF-8. | [Compatibilidad con UTF-8 en OLE DB Driver for SQL Server](features/utf-8-support-in-oledb-driver-for-sql-server.md). |
| Soporte técnico de la autenticación de Azure Active Directory. | [Uso de Azure Active Directory](features/using-azure-active-directory.md). |
| &nbsp; | &nbsp; |

## <a name="1810"></a>18.1.0

![descargar](../../ssms/media/download-icon.png) [Descargar instalador x64](https://go.microsoft.com/fwlink/?linkid=2118506)  
![descargar](../../ssms/media/download-icon.png) [Descargar instalador x86](https://go.microsoft.com/fwlink/?linkid=2118509)  

Fecha de publicación: Julio de 2018

Si necesita descargar el instalador en un idioma distinto al que se ha detectado, puede usar estos vínculos directos.  
Para el controlador x64: [Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x804) | [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x40a)  
Para el controlador x86: [Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=2118509&2118509=0x804) | [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x40a)  

### <a name="features-added-in-1810"></a>Características agregadas en la versión 18.1.0

| Característica agregada | Detalles |
| :------------ | :------ |
| Compatibilidad con la palabra clave de cadena de conexión `UseFMTONLY` y la propiedad de inicialización `SSPROP_INIT_USEFMTONLY`. | `UseFMTONLY` controla cómo se recuperan los metadatos al conectarse a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones más recientes.<br/><br/>Para más información, consulte: [Uso de palabras clave de cadena de conexión con el controlador OLE DB para SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed-in-1810"></a>Errores corregidos en la versión 18.1.0

| Error corregido | Detalles |
| :-------- | :------ |
| Se ha corregido la versión incorrecta del archivo de formato de BCP. | El controlador OLE DB 18.0 establece incorrectamente la versión del archivo de formato de BCP en 18.0, ya que el valor correcto es 11.0.<br/>El controlador OLE DB 18.1 no puede leer los archivos de formato generador por el controlador OLE DB 18.0.<br/>Si tiene que usar los archivos de formato generados por la versión anterior del controlador con el nuevo, puede editar manualmente los archivos para cambiar la versión a la 11.0. |
| &nbsp; | &nbsp; |

## <a name="1802"></a>18.0.2

![descargar](../../ssms/media/download-icon.png) [Descargar instalador x64](https://go.microsoft.com/fwlink/?linkid=2118504)  
![descargar](../../ssms/media/download-icon.png) [Descargar instalador x86](https://go.microsoft.com/fwlink/?linkid=2118277)  

Fecha de publicación: Marzo de 2018

Si necesita descargar el instalador en un idioma distinto al que se ha detectado, puede usar estos vínculos directos.  
Para el controlador x64: [Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x804) | [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x40a)  
Para el controlador x86: [Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x804) | [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x40a)  

### <a name="features-added-in-1802"></a>Características agregadas en la versión 18.0.2

| Característica agregada | Detalles |
| :------------ | :------ |
| Compatibilidad con la palabra clave de cadena de conexión `MultiSubnetFailover` y la propiedad de inicialización `SSPROP_INIT_MULTISUBNETFAILOVER`. | Para más información, consulte:<br/>&bull; &nbsp; [Compatibilidad de OLE DB Driver for SQL Server con la alta disponibilidad y la recuperación ante desastres](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)<br/>&bull; &nbsp; [Uso de palabras clave de cadena de conexión con OLE DB Driver for SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

## <a name="see-also"></a>Consulte también

[Controlador Microsoft OLE DB para SQL Server](oledb-driver-for-sql-server.md)
