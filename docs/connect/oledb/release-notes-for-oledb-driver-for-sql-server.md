---
title: Notas de la versión (Controlador OLE DB para SQL Server) | Microsoft Docs
ms.date: 10/11/2019
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: genemi
author: mateusz-kmiecik
ms.author: v-makmie
ms.openlocfilehash: 350856cc27bdec601e0db2998f9ff9953cdf6ec7
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381733"
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

Octubre de 2019

### <a name="features-added"></a>Características agregadas

| Característica agregada | Detalles |
| :------------ | :------ |
| Compatibilidad con la autenticación de Azure Active Directory (`ActiveDirectoryInteractive`, `ActiveDirectoryMSI`). | [Uso de Azure Active Directory](features/using-azure-active-directory.md). |
| Compatibilidad con Biblioteca de autenticación de Active Directory incrustado (ADAL). | Una instalación independiente de ADAL ya no es necesaria para usar determinados métodos de autenticación. |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>Errores corregidos

| Error corregido | Detalles |
| :-------- | :------ |
| Lógica de Drop index corregida en [IIndexDefinition::D ropindex](https://go.microsoft.com/fwlink/?linkid=2106448). | Las versiones anteriores del controlador de OLE DB no pueden quitar un índice de clave principal cuando el ID. de esquema y el ID. de usuario del propietario del índice no son iguales. |
| &nbsp; | &nbsp; |

## <a name="1823"></a>18.2.3

Junio de 2019

### <a name="features-added"></a>Características agregadas

| Característica agregada | Detalles |
| :------------ | :------ |
| Compatibilidad con las actualizaciones de controladores desde el SQL Server medios extraíbles. | Esta mejora permite actualizar controladores directamente desde el SQL Server medios extraíbles. |
| &nbsp; | &nbsp; |

## <a name="1822"></a>18.2.2

Mayo de 2019

### <a name="bugs-fixed"></a>Errores corregidos

| Error corregido | Detalles |
| :-------- | :------ |
| Se ha corregido un problema de interactividad en la autenticación de Azure Active Directory en contenedores multiproceso (MTA). | El controlador OLE DB 18.2.1 intenta cambiar por error el modelo de simultaneidad de COM en un contenedor previamente inicializado como multiproceso (MTA). Como resultado de esto, en una aplicación que realiza más de una llamada subsiguiente a [CoInitialize](https://go.microsoft.com/fwlink/?linkid=2092520) o [CoInitializeEx](https://go.microsoft.com/fwlink/?linkid=2092521) antes de llamar a la interfaz [IDBInitialize::Initialize](https://go.microsoft.com/fwlink/?linkid=2092522), el controlador no puede establecer una conexión al usar cualquier modo de autenticación de Azure Active Directory. |
| &nbsp; | &nbsp; |

## <a name="1821"></a>18.2.1

Febrero de 2019

### <a name="features-added"></a>Características agregadas

| Característica agregada | Detalles |
| :------------ | :------ |
| Compatibilidad con la codificación de servidor UTF-8. | [Compatibilidad con UTF-8 en OLE DB Driver for SQL Server](features/utf-8-support-in-oledb-driver-for-sql-server.md). |
| Soporte técnico de la autenticación de Azure Active Directory. | [Uso de Azure Active Directory](features/using-azure-active-directory.md). |
| &nbsp; | &nbsp; |

## <a name="1810"></a>18.1.0

Julio de 2018

### <a name="features-added"></a>Características agregadas

| Característica agregada | Detalles |
| :------------ | :------ |
| Compatibilidad con la palabra clave de cadena de conexión `UseFMTONLY` y la propiedad de inicialización `SSPROP_INIT_USEFMTONLY`. | `UseFMTONLY` controla cómo se recuperan los metadatos al conectarse a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones más recientes.<br/><br/>Para obtener más información, consulte: [usar palabras clave de cadena de conexión con OLE DB controlador para SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>Errores corregidos

| Error corregido | Detalles |
| :-------- | :------ |
| Se ha corregido la versión incorrecta del archivo de formato de BCP. | El controlador OLE DB 18.0 establece incorrectamente la versión del archivo de formato de BCP en 18.0, ya que el valor correcto es 11.0.<br/>El controlador OLE DB 18.1 no puede leer los archivos de formato generador por el controlador OLE DB 18.0.<br/>Si tiene que usar los archivos de formato generados por la versión anterior del controlador con el nuevo, puede editar manualmente los archivos para cambiar la versión a la 11.0. |
| &nbsp; | &nbsp; |

## <a name="1802"></a>18.0.2

### <a name="features-added"></a>Características agregadas

| Característica agregada | Detalles |
| :------------ | :------ |
| Compatibilidad con la palabra clave de cadena de conexión `MultiSubnetFailover` y la propiedad de inicialización `SSPROP_INIT_MULTISUBNETFAILOVER`. | Para obtener más información, vea:<br/>&bull; &nbsp; [Compatibilidad de OLE DB Driver for SQL Server con la alta disponibilidad y la recuperación ante desastres](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md),<br/>&bull; &nbsp; [Uso de palabras clave de cadena de conexión con el controlador OLE DB para SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

## <a name="see-also"></a>Vea también

[Controlador Microsoft OLE DB para SQL Server](oledb-driver-for-sql-server.md)
