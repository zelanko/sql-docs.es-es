---
title: "Actualización: Documentos de Integration Services para SQL Server | Microsoft Docs"
description: "Muestra fragmentos de contenido actualizado de documentación modificada recientemente de Integration Services para Microsoft SQL Server."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.author: genemi
ms.workload: integration-services
ms.openlocfilehash: 9660fa7239c14c3adc963cc75ceb98de8316734c
ms.sourcegitcommit: 29265ad41fbe3326c21c6908ec4275a3a38f1c09
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/04/2017
---
# <a name="new-and-recently-updated-integration-services-for-sql-server"></a>Nuevo y actualizado recientemente: Integration Services para SQL Server



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; **28-09-2017** &nbsp; a &nbsp; **02-12-2017**
- *Área de asunto:* &nbsp; **Integration Services para SQL Server**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


1. [Almacenar y recuperar archivos en recursos compartidos de archivos de forma local y en Azure con SSIS](lift-shift/ssis-azure-files-file-shares.md)
2. [Validación de paquetes de SSIS implementados en Azure](lift-shift/ssis-azure-validate-packages.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

En esta sección se muestran extractos de actualizaciones recopiladas de artículos que han sufrido una actualización importante recientemente.

Los extractos que se muestran aquí aparecen separados de su contexto semántico correcto. Además, en ocasiones, un extracto se separa de sintaxis de Markdown importante que lo rodea en el artículo real. Por tanto, estos extractos solo sirven de guía general. Los extractos solo le permiten saber si le interesa dedicar tiempo a hacer clic en el artículo real para visitarlo.

Por estas y otras razones, no copie código de estos fragmentos y no tome como verdad exacta ningún extracto de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta de artículos que se han actualizado recientemente

En esta lista compacta se proporcionan vínculos a todos los artículos actualizados que aparecen en la sección de extractos.

1. [Administrador de conexiones de Hadoop](#TitleNum_1)
2. [Conectarse a orígenes de datos locales y a recursos compartidos de archivos de Azure con la autenticación de Windows](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-hadoop-connection-managerconnection-managerhadoop-connection-managermd"></a>1. &nbsp; [Administrador de conexiones de Hadoop](connection-manager/hadoop-connection-manager.md)

*Actualizado: 28-11-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Siguiente](#TitleNum_2))

<!-- Source markdown line 65.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2d68f4e884304f1a28045b42b680c15cc6a41ec5 fb2429466ea4d545682975d8dbea47451ce98ec7  (PR=4113  ,  Filename=hadoop-connection-manager.md  ,  Dirpath=docs\integration-services\connection-manager\  ,  MergeCommitSha40=28cccac53767db70763e5e705b8cc59a83c77317) -->



**Conectar con la autenticación Kerberos**

Hay dos opciones para configurar el entorno local de forma que pueda usar la autenticación Kerberos con el administrador de conexiones de Hadoop. Puede elegir la opción que mejor se adapte a sus circunstancias.
-   Opción 1: unir el equipo SSIS al dominio Kerberos (#kerberos-join-realm)
-   Opción 2: habilitar la confianza mutua entre el dominio de Windows y el dominio Kerberos (#kerberos-mutual-trust)

**<a name="kerberos-join-realm"></a>Opción 1: unir el equipo SSIS al dominio Kerberos** 


**Requisitos:**


-   El equipo de puerta de enlace se debe unir al dominio Kerberos y no se puede unir a ningún dominio de Windows.

**Cómo se configura:**


**En el equipo SSIS:**

1.  Ejecute la utilidad **Ksetup** para configurar el dominio y el servidor KDC de Kerberos.

    El equipo debe estar configurado como miembro de un grupo de trabajo, ya que un dominio Kerberos es diferente de un dominio de Windows. Establezca el dominio Kerberos y agregue un servidor KDC como se explica en el siguiente ejemplo. Reemplace *REALM.COM* por su dominio Kerberos propio correspondiente, según sea necesario.

```
    C:> Ksetup /setdomain REALM.COM`
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
```

    Restart the computer after executing these two commands.

2.  Compruebe la configuración con el comando **Ksetup**. La salida debería ser similar a la del siguiente ejemplo:

```
    C:> Ksetup
    default realm = REALM.COM (external)
    REALM.com:
        kdc = <your_kdc_server_address>
```

**<a name="kerberos-mutual-trust"></a>Opción 2: habilitar la confianza mutua entre el dominio de Windows y el dominio Kerberos**


**Requisitos:**

-   El equipo de puerta de enlace se debe unir a un dominio de Windows.
-   Necesita permiso para actualizar la configuración del controlador de dominio.

**Cómo se configura:**


> [!NOTE]
> Reemplace REALM.COM y AD.COM en el siguiente tutorial por su dominio Kerberos y controlador de dominio propios correspondientes, según sea necesario.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-connect-to-on-premises-data-sources-and-azure-file-shares-with-windows-authenticationlift-shiftssis-azure-connect-with-windows-authmd"></a>2. &nbsp; [Conectarse a orígenes de datos locales y a recursos compartidos de archivos de Azure con la autenticación de Windows](lift-shift/ssis-azure-connect-with-windows-auth.md)

*Actualización: 27-11-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_1))

<!-- Source markdown line 66.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 673386fca53cb60b983e0cb3cd4b9e2ee1dee0de 65458b4dceb92d01184c5e9c6f68ec0e8f16ba08  (PR=4104  ,  Filename=ssis-azure-connect-with-windows-auth.md  ,  Dirpath=docs\integration-services\lift-shift\  ,  MergeCommitSha40=19e1c4067142d33e8485cb903a7a9beb7d894015) -->



**Conectarse a un servidor SQL local**

Para comprobar si puede conectarse a un servidor local de SQL Server, haga lo siguiente:

1.  Para ejecutar esta prueba, busque un equipo que no esté unido a ningún dominio.

2.  En el equipo que no esté unido a ningún dominio, ejecute el siguiente comando para iniciar SQL Server Management Studio (SSMS) con las credenciales de dominio que quiera usar:

```
    runas.exe /netonly /user:<domain>\<username> SSMS.exe
```

3.  Desde SSMS, compruebe si puede conectarse al servidor local de SQL Server que quiere usar.

**Conectarse a un recurso compartido de archivos local**

Para comprobar si puede conectarse a un recurso compartido de archivos local, haga lo siguiente:

1.  Para ejecutar esta prueba, busque un equipo que no esté unido a ningún dominio.

2.  En el equipo que no está unido a ningún dominio, ejecute el siguiente comando. Este comando abre una ventana del símbolo del sistema con las credenciales de dominio que quiera usar y, seguidamente, obtiene un listado de directorios para probar la conectividad con el recurso compartido de archivos.

```
    runas.exe /netonly /user:<domain>\<username> cmd.exe
    dir \\fileshare
```

3.  Compruebe si se devuelve la lista de directorios del recurso compartido de archivos local que quiere usar.

**Conectarse a un recurso compartido de archivos en una máquina virtual de Azure**

Haga lo siguiente para conectarse a un recurso compartido de archivos en una máquina virtual de Azure:

1.  Con SQL Server Management Studio (SSMS) u otra herramienta, conéctese a la base de datos de SQL Database que hospeda la base de datos del catálogo de SSIS (SSISDB).

2.  Con SSISDB como base de datos actual, abra una ventana de consulta.

3.  Ejecute el procedimiento almacenado `catalog.set_execution_credential` tal como se describe en las siguientes opciones:

```
    catalog.set_execution_credential @domain = N'.', @user = N'username of local account on Azure virtual machine', @password = N'password'
```

**Conectarse a un recurso compartido de archivos en Azure Files**

Para obtener más información acerca de Azure Files, consulte [Azure Files](https://azure.microsoft.com/services/storage/files/).







## <a name="similar-articles"></a>Artículos similares

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

En esta sección se enumeran artículos muy similares a los artículos actualizados recientemente en otras áreas temáticas, dentro de nuestro repositorio público de GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas temáticas con artículos nuevos o actualizados recientemente

- [Nuevos + Actualizados (3+14): documentos de **Análisis avanzado para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Nuevos + Actualizados (1+0): documentos de **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Nuevos + Actualizados (87+0): documentos de **Analytics Platform System para SQL**](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Nuevos + Actualizados (5+4): documentos de **Conexión a SQL**](../connect/new-updated-connect.md)
- [Nuevos + Actualizados (0+1): documentos de **Motor de base de datos de SQL**](../database-engine/new-updated-database-engine.md)
- [Nuevos + Actualizados (2+2): documentos de **Integration Services para SQL**](../integration-services/new-updated-integration-services.md)
- [Nuevos + Actualizados (10+9): documentos de **Linux para SQL**](../linux/new-updated-linux.md)
- [Nuevos + Actualizados (2+4): documentos de **Bases de datos relacionales para SQL**](../relational-databases/new-updated-relational-databases.md)
- [Nuevos + Actualizados (4+2): documentos de **Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Nuevos + Actualizados (0+1): documentos de **Ejemplos para SQL**](../sample/new-updated-sample.md)
- [Nuevos + Actualizados (21+0): documentos de **SQL Operations Studio**](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Nuevos + Actualizados (5+1): documentos de **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Nuevos + Actualizados (0+1): documentos de **SQL Server Data Tools (SSDT)**](../ssdt/new-updated-ssdt.md)
- [Nuevos + Actualizados (1+0): documentos de **SQL Server Migration Assistant (SSMA)**](../ssma/new-updated-ssma.md)
- [Nuevos + Actualizados (0+1): documentos de **SQL Server Management Studio (SSMS)**](../ssms/new-updated-ssms.md)
- [Nuevos + Actualizados (0+2): documentos de **Transact-SQL**](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas temáticas sin artículos nuevos ni actualizados recientemente

- [Nuevos + Actualizados (0+0): documentos de **Data Migration Assistant (DMA) para SQL**](../dma/new-updated-dma.md)
- [Nuevos + Actualizados (0+0): documentos de **Objetos de datos ActiveX (ADO) para SQL**](../ado/new-updated-ado.md)
- [Nuevos + Actualizados (0+0): documentos de **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Extensiones de minería de datos (DMX) para SQL**](../dmx/new-updated-dmx.md)
- [Nuevos + actualizados (0+0): documentos de **Master Data Services (MDS) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Expresiones multidimensionales (MDX) para SQL**](../mdx/new-updated-mdx.md)
- [Nuevos + Actualizados (0+0): documentos de **ODBC (conectividad abierta de bases de datos) para SQL**](../odbc/new-updated-odbc.md)
- [Nuevos + Actualizados (0+0): documentos de **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Nuevos + actualizados (0+0): documentos de **Herramientas para SQL**](../tools/new-updated-tools.md)
- [Nuevos + Actualizados (0+0): documentos de **XQuery para SQL**](../xquery/new-updated-xquery.md)


