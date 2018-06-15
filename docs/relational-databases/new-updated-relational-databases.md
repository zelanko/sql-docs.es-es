---
title: 'Actualizados: documentos de bases de datos relacionales | Microsoft Docs'
description: Muestra fragmentos del contenido actualizado en la documentación de bases de datos relacionales que ha cambiado recientemente.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: relational-databases
ms.date: 04/28/2018
ms.openlocfilehash: a885befe2411a76dc8c68bf2a7b543a838a52877
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32607516"
---
# <a name="new-and-recently-updated-relational-databases-docs"></a>Nuevos y actualizados recientemente: documentos de bases de datos relacionales



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; del **03-02-2018** &nbsp; al &nbsp; **28-04-2018**
- *Área temática:* &nbsp; **Bases de datos relacionales**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


1. [Combinaciones (SQL Server)](performance/joins.md)
2. [Subconsultas (SQL Server)](performance/subqueries.md)
3. [Configurar la base de datos de distribución de replicación en un grupo de disponibilidad AlwaysOn](replication/configure-distribution-availability-group.md)
4. [Clasificación y detección de datos de SQL](security/sql-data-discovery-and-classification.md)
5. [Guía de versiones de fila y bloqueo de transacciones](sql-server-transaction-locking-and-row-versioning-guide.md)
6. [sys.dm_os_job_object (Azure SQL Database)](system-dynamic-management-views/sys-dm-os-job-object-transact-sql.md)
7. [Procedimientos almacenados del sistema de Filestream y FileTable (Transact-SQL)](system-stored-procedures/filestream-and-filetable-system-stored-procedures.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

En esta sección se muestran extractos de actualizaciones recopiladas de artículos que han sufrido una actualización importante recientemente.

Los extractos que se muestran aquí aparecen separados de su contexto semántico correcto. Además, en ocasiones, un extracto se separa de sintaxis de Markdown importante que lo rodea en el artículo real. Por tanto, estos extractos solo sirven de guía general. Los extractos solo le permiten saber si le interesa dedicar tiempo a hacer clic en el artículo real para visitarlo.

Por estas y otras razones, no copie código de estos fragmentos y no tome como verdad exacta ningún extracto de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta de artículos que se han actualizado recientemente

En esta lista compacta se proporcionan vínculos a todos los artículos actualizados que aparecen en la sección de extractos.

1. [Usar un archivo de formato para omitir una columna de tabla (SQL Server)](#TitleNum_1)
2. [Datos JSON en SQL Server](#TitleNum_2)
3. [Guía de arquitectura de procesamiento de consultas](#TitleNum_3)
4. [Tutorial: Preparar SQL Server para la replicación: publicador, distribuidor, suscriptor](#TitleNum_4)
5. [Tutorial: Configurar la replicación entre dos servidores conectados de forma continua (transaccional)](#TitleNum_5)
6. [Tutorial: Configurar la replicación entre un servidor y clientes móviles (de mezcla)](#TitleNum_6)
7. [Consultar con búsqueda de texto completo](#TitleNum_7)
8. [Cifrado de datos transparente compatible con Bring Your Own Key para Azure SQL Database y SQL Data Warehouse](#TitleNum_8)
9. [PowerShell y CLI: Habilitar el Cifrado de datos transparente con su propia clave desde Azure Key Vault](#TitleNum_9)
10. [Acerca de la captura de datos modificados (SQL Server)](#TitleNum_10)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-use-a-format-file-to-skip-a-table-column-sql-serverimport-exportuse-a-format-file-to-skip-a-table-column-sql-servermd"></a>1. &nbsp;[Usar un archivo de formato para omitir una columna de tabla (SQL Server)](import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)

*Actualizado: 13-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Siguiente](#TitleNum_2))

<!-- Source markdown line 221.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 167916d79c5de1e7f13990cb7acc41ceb541b9a7 cb92eb201292294e3397879c98f353fba45f1c1c  (PR=0  ,  Filename=use-a-format-file-to-skip-a-table-column-sql-server.md  ,  Dirpath=docs\relational-databases\import-export\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



**Usar OPENROWSET(BULK...)**


Para usar un archivo de formato XML para omitir una columna de tabla mediante el uso de `OPENROWSET(BULK...)`, debe proporcionar una lista explícita de las columnas en la lista de selección y en la tabla de destino de la siguiente forma:

```
    INSERT ...<column_list> SELECT <column_list> FROM OPENROWSET(BULK...)
```

En el siguiente ejemplo se utiliza el proveedor de conjuntos de filas BULK `OPENROWSET` y el archivo de formato `myTestSkipCol2.xml` . En el ejemplo se importa masivamente el archivo de datos `myTestSkipCol2.dat` a la tabla `myTestSkipCol` . La instrucción contiene una lista explícita de las columnas en la lista de selección y también en la tabla de destino, según convenga.

En SSMS, ejecute el código siguiente. Actualice las rutas del sistema de archivos a la ubicación de los archivos de ejemplo del equipo.

```
USE WideWorldImporters;
GO
INSERT INTO myTestSkipCol
  (Col1,Col3)
    SELECT Col1,Col3
      FROM  OPENROWSET(BULK  'C:\myTestSkipCol2.Dat',
      FORMATFILE='C:\myTestSkipCol2.Xml'
       ) as t1 ;
GO
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-json-data-in-sql-serverjsonjson-data-sql-servermd"></a>2. &nbsp; [Datos JSON en SQL Server](json/json-data-sql-server.md)

*Actualizado: 13-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_1) | [Siguiente](#TitleNum_3))

<!-- Source markdown line 145.  ms.author= "jovanpop".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 19e276637a463b412f2c29a84f9fb7d0b0f5fcc5 e2f2e8b4732779b3f24561cc0c4da3a958f4edbb  (PR=0  ,  Filename=json-data-sql-server.md  ,  Dirpath=docs\relational-databases\json\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



Los documentos JSON pueden tener subelementos y datos jerárquicos que no se pueden asignar directamente a las columnas relacionales estándares. En este caso, es posible simplificar la jerarquía JSON mediante la combinación de la entidad primaria con submatrices.

En el ejemplo siguiente, el segundo objeto de la matriz tiene una submatriz que representa las aptitudes de una persona. Todos los objetos secundarios se pueden analizar mediante una llamada adicional a la función `OPENJSON`:

```
DECLARE @json NVARCHAR(MAX)
SET @json =
N'[
       { "id" : 2,"info": { "name": "John", "surname": "Smith" }, "age": 25 },
       { "id" : 5,"info": { "name": "Jane", "surname": "Smith", "skills": ["SQL", "C#", "Azure"] }, "dob": "2005-11-04T12:00:00" }
 ]'

SELECT *
FROM OPENJSON(@json)
  WITH (id int 'strict $.id',
        firstName nvarchar(50) '$.info.name', lastName nvarchar(50) '$.info.surname',
        age int, dateOfBirth datetime2 '$.dob',
    skills nvarchar(max) '$.skills' as json)
    outer apply openjson( a.skills )
                     with ( skill nvarchar(8) '$' ) as b
```
La matriz **aptitudes** se devuelve en la primera `OPENJSON` como el fragmento de texto JSON original y se pasa a otra función `OPENJSON` mediante el operador `APPLY`. La segunda función `OPENJSON` analizará la matriz JSON y los valores de cadena devueltos como un conjunto de filas de una columna única que se combinarán con el resultado de la primera `OPENJSON`.
El resultado de esta consulta se muestra en la tabla siguiente:

**Resultado**

|id|firstName|lastName|age|dateOfBirth|aptitudes|
|--------|---------------|--------------|---------|-----------------|----------|
|2|John|Smith|25|||
|5|Jane|Smith||2005-11-04T12:00:00|SQL|
|5|Jane|Smith||2005-11-04T12:00:00|C#|
|5|Jane|Smith||2005-11-04T12:00:00|Azure|

`OUTER APPLY OPENJSON` se unirá a la entidad de primer nivel con la submatriz y devolverá un conjunto de resultados sin formato. Debido a JOIN, la segunda fila se repetirá para cada aptitud.




&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-query-processing-architecture-guidequery-processing-architecture-guidemd"></a>3. &nbsp; [Guía de arquitectura de procesamiento de consultas](query-processing-architecture-guide.md)

*Actualizado: 13-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_2) | [Siguiente](#TitleNum_4))

<!-- Source markdown line 34.  ms.author= "jroth".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 96d91b39acdb2f32aaff323e374e92d6f229d241 2c1d2f8585632ada174388399782dc3ed2721dba  (PR=0  ,  Filename=query-processing-architecture-guide.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



**Prioridad de los operadores lógicos**


Cuando en una instrucción se usa más de un operador lógico, primero se evalúa `NOT`, luego `AND` y, finalmente, `OR`. Los operadores aritméticos y bit a bit se tratan antes que los operadores lógicos. Para más información, consulte [Prioridad de operador].

En el siguiente ejemplo, la condición de color pertenece al modelo de producto 21 y no al modelo de producto 20, ya que porque `AND` tiene prioridad sobre `OR`.

```
SELECT ProductID, ProductModelID
FROM Production.Product
WHERE ProductModelID = 20 OR ProductModelID = 21
  AND Color = 'Red';
GO
```

Puede cambiar el significado de la consulta si agrega paréntesis para provocar que `OR` se evalúe primero. La siguiente consulta busca solamente los productos en los modelos 20 y 21 que sean rojos.

```
SELECT ProductID, ProductModelID
FROM Production.Product
WHERE (ProductModelID = 20 OR ProductModelID = 21)
  AND Color = 'Red';
GO
```

El uso de paréntesis, incluso cuando no se necesitan, puede mejorar la comprensión de las consultas y reducir las posibilidades de cometer un error debido a la prioridad de los operadores. No hay ninguna reducción significativa del rendimiento que sea achacable al uso de paréntesis. El siguiente ejemplo se lee mejor que el ejemplo original, aunque ambos son sintácticamente iguales.

```
SELECT ProductID, ProductModelID
FROM Production.Product
WHERE ProductModelID = 20 OR (ProductModelID = 21
  AND Color = 'Red');
GO
```




&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-tutorial-prepare-sql-server-for-replication---publisher-distributor-subscriberreplicationtutorial-preparing-the-server-for-replicationmd"></a>4. &nbsp; [Tutorial: Preparación de SQL Server para la replicación: publicador, distribuidor, suscriptor](replication/tutorial-preparing-the-server-for-replication.md)

*Actualizado: 13-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_3) | [Siguiente](#TitleNum_5))

<!-- Source markdown line 56.  ms.author= "mathoma".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 6e5caedacff193ce79bdd98708ae1b9dc91f0a8f 9f7af4d3f8b1cffd048db2a5b29fc9e6013f5ed2  (PR=0  ,  Filename=tutorial-preparing-the-server-for-replication.md  ,  Dirpath=docs\relational-databases\replication\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



- Instale [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
- Instale [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
- Descargar una [Base de datos de ejemplo AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases). Para obtener instrucciones sobre cómo restaurar una base de datos en SSMS, vea [Restaurar una base de datos](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms).

>[!NOTE]
> - La replicación no se admite entre SQL Server que estén separados por más de dos versiones entre sí. Para obtener más información, vea [Versiones de SQL admitidas en la topología de replicación](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/).
> - En *{Included-Content-Goes-Here}*, debe conectarse al publicador y al suscriptor con un inicio de sesión que sea miembro del rol fijo de servidor **sysadmin**. Para obtener más información sobre el rol sysadmin, vea [Roles de nivel de servidor](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/server-level-roles).


**Tiempo estimado para completar este tutorial: 30 minutos**

**Creación de cuentas de Windows para replicación**

En esta sección creará cuentas de Windows para ejecutar agentes de replicación. Creará distintas cuentas de Windows en el servidor local para los siguientes agentes:

|Agente|Ubicación|Nombre de cuenta|
|---------|------------|----------------|
|Agente de instantáneas|publicador|<*nombreDeEquipo*>\repl_snapshot|



&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-tutorial-configure-replication-between-two-fully-connected-servers-transactionalreplicationtutorial-replicating-data-between-continuously-connected-serversmd"></a>5. &nbsp; [Tutorial: Configuración de la replicación entre dos servidores conectados de forma continua (transaccional)](replication/tutorial-replicating-data-between-continuously-connected-servers.md)

*Actualizado: 13-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_4) | [Siguiente](#TitleNum_6))

<!-- Source markdown line 162.  ms.author= "mathoma".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0d74f984d0ffc01cce0376837e6d94df3c5654d7 4ecf4d724286130927dd43687d6845059af6f9b7  (PR=0  ,  Filename=tutorial-replicating-data-between-continuously-connected-servers.md  ,  Dirpath=docs\relational-databases\replication\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



**Creación de una suscripción a la publicación transaccional**

En esta sección, agregará un suscriptor a la publicación que creada anteriormente. Este tutorial utiliza un suscriptor remoto (NODE2\SQL2016), pero también puede agregarse una suscripción localmente en el publicador.

**Para crear la suscripción**


1.  Conéctese al publicador en *{Included-Content-Goes-Here}*, expanda el nodo del servidor y luego la carpeta **Replicación**.

2.  En la carpeta **Publicaciones locales**, haga clic con el botón derecho en la publicación **AdvWorksProductTrans** y, después, seleccione **Nuevas suscripciones**.  Se iniciará el Asistente para nueva suscripción:

    Nueva suscripción

3.  En la página Publicación, seleccione **AdvWorksProductTrans** y, a continuación, seleccione **Siguiente**:

    Seleccione el publicador de transacciones

4.  En la página Ubicación del Agente de distribución, seleccione **Ejecutar todos los agentes en el distribuidor** y luego seleccione **Siguiente**.  Para más información sobre las suscripciones de inserción y de extracción, vea [Suscribirse a publicaciones](https://docs.microsoft.com/sql/relational-databases/replication/subscribe-to-publications):

    Ejecutar Agentes de distribución

5.  En la página Suscriptores, si no se muestra el nombre de la instancia del suscriptor, seleccione **Agregar suscriptor** y, después, seleccione **Agregar suscriptor de SQL Server** en la lista desplegable. Esto abrirá el cuadro de diálogo **Conectar al servidor**. Escriba el nombre de instancia del suscriptor y, después, seleccione **Conectar**.



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-tutorial-configure-replication-between-a-server-and-mobile-clients-mergereplicationtutorial-replicating-data-with-mobile-clientsmd"></a>6. &nbsp; [Tutorial: Configurar la replicación entre un servidor y clientes móviles (combinación)](replication/tutorial-replicating-data-with-mobile-clients.md)

*Actualizado: 13-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_5) | [Siguiente](#TitleNum_7))

<!-- Source markdown line 93.  ms.author= "mathoma".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0eed78dfe83c88358c030539a2b25d11ef5ec2d3 79b2a3f32c940fede94b11ad2a3ef8a00b911a39  (PR=0  ,  Filename=tutorial-replicating-data-with-mobile-clients.md  ,  Dirpath=docs\relational-databases\replication\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



La tabla Employee contiene una columna (OrganizationNode) que tiene el tipo de datos hierarchyid, que solo se admite para la replicación en SQL 2017. Si usa una versión anterior a SQL 2017, verá un mensaje en la parte inferior de la pantalla que le notifica de posibles pérdidas de datos si usa esta columna en la replicación bidireccional. Para los fines de este tutorial, puede hacer caso omiso de este mensaje. Pero este tipo de datos no debería replicarse en un entorno de producción a menos que esté usando la versión compatible. Para obtener más información sobre cómo replicar el tipo de datos hierarchyid, vea [Usar columnas Hierarchyid en la replicación](https://docs.microsoft.com/sql/t-sql/data-types/hierarchyid-data-type-method-reference#using-hierarchyid-columns-in-replicated-tables)


-  En la página Filtrar filas de tabla, seleccione **Agregar** y luego **Agregar filtro**.

-  En el cuadro de diálogo **Agregar filtro**, seleccione **Employee (HumanResources)** en **Seleccione la tabla que desea filtrar**. Seleccione la columna **LoginID**, seleccione la flecha derecha para agregar la columna a la cláusula WHERE de la consulta del filtro y modifique la cláusula WHERE de la manera siguiente:

    ```
    WHERE [LoginID] = HOST_NAME()
    ```

    A. Seleccione **Una fila de esta tabla irá a una sola suscripción**y luego **Aceptar**:

    Agregar filtro



- En la página **Filtrar filas de tabla**, seleccione **Employee (Human Resources)**, luego **Agregar** y, después, **Agregar combinación para ampliar el filtro seleccionado**.

    A. En el cuadro de diálogo **Agregar combinación**, seleccione **Sales.SalesOrderHeader** en **Tabla combinada**. Seleccione **Escribir instrucción de combinación manualmente** y complete la instrucción de combinación de la manera siguiente:



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-query-with-full-text-searchsearchquery-with-full-text-searchmd"></a>7. &nbsp; [Consultar con búsqueda de texto completo](search/query-with-full-text-search.md)

*Actualizado: 13-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_6) | [Siguiente](#TitleNum_8))

<!-- Source markdown line 247.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5ec67b56aa0a6eadadbcfa8b73b6726e75eca2bb 4eb108b202d3dd035a312bac7872cf02bcf31cfa  (PR=0  ,  Filename=query-with-full-text-search.md  ,  Dirpath=docs\relational-databases\search\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



**Más información sobre la generación de términos de búsqueda**


Las *formas con inflexión* son los distintos tiempos y conjugaciones de un verbo o las formas singular y plural de un nombre.

Por ejemplo, busque la forma con inflexión de la palabra "drive". Si hay varias filas en la tabla que incluyan las palabras "drive", "drives", "drove", "driving" y "driven", todas estarían en el conjunto de resultados porque cada una de estas palabras se puede generar a partir de la palabra "drive".

[FREETEXT] y [FREETEXTTABLE] buscan términos con inflexión de todas las palabras especificadas de forma predeterminada. [CONTAINS] y [CONTAINSTABLE] admiten un argumento `INFLECTIONAL` opcional.

**Búsqueda de sinónimos de una palabra específica**


Un *diccionario de sinónimos* define los sinónimos especificados por el usuario para los términos. Para más información sobre los archivos de diccionario de sinónimos, consulte [Configurar y administrar archivos de sinónimos para búsquedas de texto completo].

Por ejemplo, si una entrada, "{car, automobile, truck, van}", se agrega a un diccionario de sinónimos, puede buscar la forma sinónima de la palabra "car". Todas las filas de la tabla consultada que incluyen las palabras "automobile", "truck", "van" o "car" aparecen en el conjunto de resultados porque cada una de estas palabras pertenece al conjunto de expansión de sinónimos de la palabra "car".

[FREETEXT] y [FREETEXTTABLE] usan el diccionario de sinónimos de forma predeterminada. [CONTAINS] y [CONTAINSTABLE] admiten un argumento `THESAURUS` opcional.



&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-transparent-data-encryption-with-bring-your-own-key-support-for-azure-sql-database-and-data-warehousesecurityencryptiontransparent-data-encryption-byok-azure-sqlmd"></a>8. &nbsp; [Cifrado de datos transparente compatible con Bring Your Own Key para Azure SQL Database y SQL Data Warehouse](security/encryption/transparent-data-encryption-byok-azure-sql.md)

*Actualizado: 24-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_7) | [Siguiente](#TitleNum_9))

<!-- Source markdown line 110.  ms.author= "aliceku".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9527658848d430bf0148be84474a75b232cbd112 70ed2a129c580962384f808e8526673957f00d2c  (PR=5662  ,  Filename=transparent-data-encryption-byok-azure-sql.md  ,  Dirpath=docs\relational-databases\security\encryption\  ,  MergeCommitSha40=91a9c812739a1c9a6ec9e7b8cda71ee1f5adae3d) -->



**Cómo configurar Geo-DR con Azure Key Vault**


Para conservar la alta disponibilidad de los protectores del TDE en las bases de datos cifradas, es necesario configurar almacenes de Azure Key Vault redundantes a partir de los grupos de conmutación por error de SQL Database o de las instancias de replicación geográfica activas existentes o deseados.  Cada servidor con replicación geográfica requiere un almacén de claves distinto, que debe estar colocado con el servidor en la misma región de Azure. En el caso de que una base de datos principal deje de ser accesible debido a una interrupción en una región y que se desencadene una conmutación por error, la base de datos secundaria podrá encargarse usando el almacén de claves secundario.

En el caso de las bases de datos SQL de Azure con replicación geográfica, se necesita la siguiente configuración de Azure Key Vault:
- Una base de datos principal con un almacén de claves ubicado en la región y una base de datos secundaria con un almacén de claves ubicado en la región.
- Se necesita como mínimo una base de datos secundaria (se admiten hasta cuatro bases de datos secundarias).
- No se admiten las bases de datos secundarias de bases de datos secundarias (encadenamiento).

En la siguiente sección se tratan con más detalle los pasos de instalación y configuración.

**Pasos de configuración de Azure Key Vault**


- Instale [PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-5.6.0).
- Cree dos almacenes de Azure Key Vault en dos regiones diferentes mediante [PowerShell para habilitar la propiedad "soft-delete"](https://docs.microsoft.com/azure/key-vault/key-vault-soft-delete-powershell) en los almacenes de claves (esta opción aún no está disponible desde el portal de Azure Key Vault, pero la requiere SQL).
- Los dos almacenes de Azure Key Vault deben estar ubicados en las dos regiones disponibles de la misma ubicación geográfica de Azure para que la copia de seguridad y la restauración de las claves funcionen.  Si necesita que los dos almacenes de claves estén en zonas geográficas diferentes para cumplir los requisitos de Geo-DR de SQL, siga el [proceso BYOK](https://docs.microsoft.com/azure/key-vault/key-vault-hsm-protected-keys) que permite importar las claves desde un HSM local.



&nbsp;

&nbsp;

---

<a name="TitleNum_9"/>

### <a name="9-nbsp-powershell-and-cli-enable-transparent-data-encryption-using-your-own-key-from-azure-key-vaultsecurityencryptiontransparent-data-encryption-byok-azure-sql-configuremd"></a>9. &nbsp; [PowerShell y CLI: Habilitar el Cifrado de datos transparente con su propia clave desde Azure Key Vault](security/encryption/transparent-data-encryption-byok-azure-sql-configure.md)

*Actualizado: 24-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_8) | [Siguiente](#TitleNum_10))

<!-- Source markdown line 196.  ms.author= "aliceku".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a0e00f5701d9a493f503a477c69097ce65aba174 721e8fb856a55ee1e8e9e7fc06036a03adab647b  (PR=5662  ,  Filename=transparent-data-encryption-byok-azure-sql-configure.md  ,  Dirpath=docs\relational-databases\security\encryption\  ,  MergeCommitSha40=91a9c812739a1c9a6ec9e7b8cda71ee1f5adae3d) -->



**Requisitos previos de CLI**


- Debe tener una suscripción de Azure y debe ser administrador en esa suscripción.
- [Recomendado pero opcional] Debería tener un módulo de seguridad de hardware (HSM) o un almacén de claves locales para crear una copia local del material de la clave del protector del TDE.
- Versión 2.0 o posterior de la interfaz de línea de comandos. Para instalar la versión más reciente y poder conectarse a su suscripción de Azure, vea [Instalación y configuración de la interfaz de línea de comandos multiplataforma de Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).
- Debe crear un almacén de Azure Key Vault y una clave para usarlos para el TDE.
   - [Administración de Key Vault mediante CLI 2.0](https://docs.microsoft.com/azure/key-vault/key-vault-manage-with-cli2)
   - [Instrucciones para usar un módulo de seguridad de hardware (HSM) y Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-get-started#a-idhsmaif-you-want-to-use-a-hardware-security-module-hsm)
 - Key Vault debe tener la siguiente propiedad, que se va a usar para el TDE:
   - [Eliminación temporal](https://docs.microsoft.com/azure/key-vault/key-vault-ovw-soft-delete)
   - [Uso de la eliminación temporal de Key Vault con la CLI](https://docs.microsoft.com/azure/key-vault/key-vault-soft-delete-cli)
- La clave debe tener los siguientes atributos que se usarán para el TDE:
   - Sin fecha de expiración
   - No deshabilitado
   - Debe poder llevar a cabo las operaciones *get*, *wrap key* y *unwrap key*.

**Paso: Creación de un servidor y asignación de una identidad de Azure AD al servidor**

      cli
      # create server (with identity) and database



&nbsp;

&nbsp;

---

<a name="TitleNum_10"/>

### <a name="10-nbsp-about-change-data-capture-sql-servertrack-changesabout-change-data-capture-sql-servermd"></a>10. &nbsp; [Acerca de la captura de datos modificados (SQL Server)](track-changes/about-change-data-capture-sql-server.md)

*Actualizado: 17-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_9))

<!-- Source markdown line 112.  ms.author= "jroth".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 588bff652adefd719e799e9777a416b70184c5f8 77ebdbb1b98b24054d5c5afbb3f1d40e94d1e6bc  (PR=5574  ,  Filename=about-change-data-capture-sql-server.md  ,  Dirpath=docs\relational-databases\track-changes\  ,  MergeCommitSha40=bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68) -->



**Trabajar con diferencias de intercalación de base de datos y de tabla**


Es importante ser consciente de un caso en el que se tienen distintas intercalaciones entre la base de datos y las columnas de una tabla configurada para la captura de datos modificados. La captura de datos modificados usa el almacenamiento provisional para rellenar las tablas laterales. Si una tabla tiene columnas CHAR o VARCHAR con intercalaciones que son diferentes de la intercalación de base de datos y esas columnas almacenan caracteres que no son ASCII (por ejemplo, caracteres DBCS de doble byte), es posible que la captura de datos modificados no pueda conservar los datos modificados de manera coherente con los datos de las tablas base. Esto se debe a que las variables del almacenamiento provisional no pueden tener intercalaciones asociadas a estas.

Plantéese la posibilidad de aplicar uno de los siguientes métodos para asegurarse de que la captura de datos modificados sea coherente con las tablas base:

- Use el tipo de datos NCHAR o NVARCHAR para las columnas que contienen datos que no sean ASCII.

- También puede usar la misma intercalación para las columnas y para la base de datos.

Por ejemplo, si tiene una base de datos que usa una intercalación de SQL_Latin1_General_CP1_CI_AS, observe la siguiente tabla:

```
CREATE TABLE T1(
     C1 INT PRIMARY KEY,
     C2 VARCHAR(10) collate Chinese_PRC_CI_AI)
```

La captura de datos modificados podría no capturar los datos binarios de la columna C2, dado que su intercalación es diferente (Chinese_PRC_CI_AI). Use NVARCHAR para evitar este problema:

```
CREATE TABLE T1(
     C1 INT PRIMARY KEY,
     C2 NVARCHAR(10) collate Chinese_PRC_CI_AI --Unicode data type, CDC works well with this data type)
```







## <a name="similar-articles-about-new-or-updated-articles"></a>Artículos similares sobre artículos nuevos o actualizados

En esta sección se enumeran artículos muy similares a los artículos actualizados recientemente en otras áreas temáticas, dentro de nuestro repositorio público de GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Áreas temáticas *con* artículos nuevos o actualizados recientemente

- [Nuevos + actualizados (11+6): documentos de &nbsp;&nbsp;**Análisis avanzado para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Nuevos + actualizados (18+0): documentos de &nbsp;&nbsp;**Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Nuevos + actualizados (218+14): documentos de **Conexión a SQL**](../connect/new-updated-connect.md)
- [Nuevos + actualizados (14+0): documentos del &nbsp;&nbsp;**Motor de base de datos de SQL**](../database-engine/new-updated-database-engine.md)
- [Nuevos + actualizados (3+2): documentos de &nbsp;&nbsp;**Integration Services para SQL**](../integration-services/new-updated-integration-services.md)
- [Nuevos + actualizados (3+3): documentos de &nbsp;&nbsp;**Linux para SQL**](../linux/new-updated-linux.md)
- [Nuevos + actualizados (7+10): documentos de&nbsp;&nbsp;**Bases de datos relacionales para SQL**](../relational-databases/new-updated-relational-databases.md)
- [Nuevos + actualizados (0+2): documentos de &nbsp;&nbsp;**Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Nuevos + actualizados (1+3): documentos de &nbsp;&nbsp;**SQL Operations Studio**](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Nuevos + actualizados (2+3): documentos de &nbsp;&nbsp;**Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Nuevos + actualizados (1+1): documentos de &nbsp;&nbsp;**SQL Server Data Tools (SSDT)**](../ssdt/new-updated-ssdt.md)
- [Nuevos + actualizados (5+2): documentos de &nbsp;&nbsp;**SQL Server Management Studio (SSMS)**](../ssms/new-updated-ssms.md)
- [Nuevos + actualizados (0+2): documentos de &nbsp;&nbsp;**Transact-SQL**](../t-sql/new-updated-t-sql.md)
- [Nuevos + actualizados (1+1): documentos de &nbsp;&nbsp;**Herramientas para SQL**](../tools/new-updated-tools.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Áreas temáticas que *no* tienen artículos nuevos o actualizados recientemente

- [Nuevos + actualizados (0+0): documentos de **Analytics Platform System para SQL**](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Nuevos + Actualizados (0+0): documentos de **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Extensiones de minería de datos (DMX) para SQL**](../dmx/new-updated-dmx.md)
- [Nuevos + actualizados (0+0): documentos de **Master Data Services (MDS) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Expresiones multidimensionales (MDX) para SQL**](../mdx/new-updated-mdx.md)
- [Nuevos + Actualizados (0+0): documentos de **ODBC (conectividad abierta de bases de datos) para SQL**](../odbc/new-updated-odbc.md)
- [Nuevos + Actualizados (0+0): documentos de **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Nuevos + Actualizados (0+0): documentos de **Ejemplos para SQL**](../samples/new-updated-samples.md)
- [Nuevos + Actualizados (0+0): documentos de **SQL Server Migration Assistant (SSMA)**](../ssma/new-updated-ssma.md)
- [Nuevos + Actualizados (0+0): documentos de **XQuery para SQL**](../xquery/new-updated-xquery.md)

