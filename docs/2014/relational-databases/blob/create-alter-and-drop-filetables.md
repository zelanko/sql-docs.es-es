---
title: Creación, modificación y eliminación de FileTables | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], altering
- FileTables [SQL Server], dropping
- FileTables [SQL Server], creating
ms.assetid: 47d69e37-8778-4630-809b-2261b5c41c2c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b810a3785c41356042639c4fdb79b4f6cf28d871
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "76934797"
---
# <a name="create-alter-and-drop-filetables"></a>Crear, modificar y quitar FileTables
  Describe cómo crear una nueva FileTable. O bien, modificar o quitar una FileTable existente.  
  
##  <a name="BasicsCreate"></a>Crear una FileTable  
 Una FileTable es una tabla de usuario especializada que tiene un esquema predefinido y fijo. Este esquema almacena los datos FILESTREAM, la información de directorios y archivos, así como los atributos de archivos. Para obtener información acerca del esquema de FileTable, vea [FileTable Schema](filetable-schema.md).  
  
 Puede crear una nueva FileTable con Transact-SQL o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Puesto que una FileTable tiene un esquema fijo, no tiene que especificar ninguna lista de columnas. La sintaxis simple para crear una FileTable permite especificar:  
  
-   Un nombre de directorio. En la jerarquía de carpetas de FileTable, este directorio de nivel de tabla se convierte en el elemento secundario del directorio de la base de datos especificado en el nivel de base de datos y en el elemento primario de los archivos o directorios almacenados en la tabla.  
  
-   El nombre de la intercalación que se va usar para los nombres de archivo en la columna **Name** de la FileTable.  
  
-   Los nombres que se van a utilizar para la clave principal 3 y las restricciones únicas que se crean automáticamente.  
  
###  <a name="HowToCreate"></a>Cómo: crear una FileTable  
 **Crear una FileTable mediante Transact-SQL**  
 Cree una FileTable llamando a la instrucción [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql) con la opción **AS FileTable**. Puesto que una FileTable tiene un esquema fijo, no tiene que especificar ninguna lista de columnas. Puede especificar los siguientes valores para la nueva FileTable:  
  
1.  **FILETABLE_DIRECTORY**. Especifica el directorio que actúa como directorio raíz de todos los archivos y directorios almacenados en la FileTable. Este nombre debe ser único entre todos los nombres de directorio de FileTable en la base de datos. La comparación de unicidad no distingue mayúsculas de minúsculas, independientemente de la configuración de intercalación actual.  
  
    -   Este valor tiene un tipo de datos de **nvarchar(255)** y usa una intercalación fija de **Latin1_General_CI_AS_KS_WS**.  
  
    -   El nombre de directorio que proporcione debe cumplir los requisitos del sistema de archivos de un nombre de directorio válido.  
  
    -   Este nombre debe ser único entre todos los nombres de directorio de FileTable en la base de datos. La comparación de unicidad no distingue mayúsculas de minúsculas, independientemente de la configuración de intercalación actual.  
  
    -   Si no proporciona un nombre de directorio al crear la FileTable, su nombre se usa como el del directorio.  
  
2.  **FILETABLE_COLLATE_FILENAME**. Especifica el nombre de la intercalación que se va a aplicar a la columna **Name** en la FileTable.  
  
    1.  La intercalación especificada **no debe distinguir mayúsculas de minúsculas** para cumplir la semántica de nomenclatura de archivo de Windows.  
  
    2.  Si no proporciona un valor para **FILETABLE_COLLATE_FILENAME**o especifica **database_default**, la columna hereda la intercalación de la base de datos actual. Si la intercalación de la base de datos actual distingue mayúsculas de minúsculas, se produce un error en la operación **CREATE TABLE** .  
  
3.  También puede especificar los nombres que se van a utilizar para la clave principal 3 y las restricciones únicas que se crean automáticamente. Si no proporciona nombres, el sistema generará los nombres cómo se describe más adelante en este tema.  
  
    -   **FILETABLE_PRIMARY_KEY_CONSTRAINT_NAME**  
  
    -   **FILETABLE_STREAMID_UNIQUE_CONSTRAINT_NAME**  
  
    -   **FILETABLE_FULLPATH_UNIQUE_CONSTRAINT_NAME**  
  
 **Ejemplos**  
  
 En el ejemplo siguiente se crea una nueva FileTable y se especifican valores definidos por el usuario para **FILETABLE_DIRECTORY** y **FILETABLE_COLLATE_FILENAME**.  
  
```sql  
CREATE TABLE DocumentStore AS FileTable  
    WITH (   
          FileTable_Directory = 'DocumentTable',  
          FileTable_Collate_Filename = database_default  
         );  
GO  
```  
  
 El siguiente ejemplo también crea una nueva FileTable. Puesto que no se especifican valores definidos por el usuario, el valor de **FILETABLE_DIRECTORY** se convierte en el nombre de la FileTable, el valor de **FILETABLE_COLLATE_FILENAME** se convierte en database_default y la clave principal y las restricciones únicas reciben nombres generados por el sistema.  
  
```sql  
CREATE TABLE DocumentStore AS FileTable;  
GO  
```  
  
 **Crear una FileTable mediante SQL Server Management Studio**  
 En el Explorador de objetos, expanda los objetos situados debajo de la base de datos seleccionada, haga clic con el botón derecho en la carpeta **Tablas** y, luego, seleccione **Nueva FileTable**.  
  
 Esta opción abre una nueva ventana de script que contiene una plantilla de script Transact-SQL que puede personalizar y ejecutar para crear una FileTable. Use la opción **Especificar valores para parámetros de plantilla** en el menú **Consulta** para personalizar el script fácilmente.  
  
###  <a name="ReqCreate"></a>Requisitos y restricciones para crear una FileTable  
  
-   No puede modificar una tabla existente para convertirla en una FileTable.  
  
-   El directorio primario especificado anteriormente en el nivel de base de datos debe tener un valor distinto de NULL. Para obtener información sobre cómo especificar el directorio de nivel de base de datos, vea [Habilitar los requisitos previos de FileTables](enable-the-prerequisites-for-filetable.md).  
  
-   Una FileTable requiere un grupo de archivos FILESTREAM válido, ya que una FileTable contiene una columna FILESTREAM. Opcionalmente, puede especificar un grupo de archivos FILESTREAM válido como parte del comando **CREATE TABLE** para crear una FileTable. Si no especifica ningún grupo de archivos, la FileTable usa el grupo de archivos FILESTREAM predeterminado para la base de datos. Si la base de datos no tiene ningún grupo de archivos FILESTREAM, se produce un error.  
  
-   No puede crear ninguna restricción de tabla como parte de una instrucción **CREATE TABLE...AS FILETABLE**. No obstante, puede agregar la restricción más tarde con una instrucción **ALTER TABLE** .  
  
-   No puede crear ninguna FileTable en la base de datos **tempdb** ni en ninguna de la demás bases de datos del sistema.  
  
-   No puede crear ninguna FileTable como tabla temporal.  
  
##  <a name="BasicsAlter"></a>Modificar una FileTable  
 Puesto que una FileTable tiene un esquema predefinido y fijo, no puede agregar ni cambiar sus columnas. No obstante, puede agregar índices personalizados, desencadenadores, restricciones y opciones adicionales a una FileTable.  
  
 Para obtener información sobre el uso de la instrucción ALTER TABLE para habilitar o deshabilitar el espacio de nombres de FileTable, incluidas las restricciones definidas por el sistema, vea [Administrar FileTables](manage-filetables.md).  
  
###  <a name="HowToChange"></a>Cómo: cambiar el directorio de una FileTable  
 **Cambiar el directorio de un objeto FileTable mediante Transact-SQL**  
 Llame a la instrucción ALTER TABLE y proporcione un nuevo valor válido para la opción **FILETABLE_DIRECTORY** SET.  
  
 **Ejemplo**  
  
```sql  
ALTER TABLE filetable_name  
    SET ( FILETABLE_DIRECTORY = N'directory_name' );  
GO  
```  
  
 **Cambiar el directorio de una FileTable mediante SQL Server Management Studio**  
 En el Explorador de objetos, haga clic con el botón derecho en el objeto FileTable y seleccione **Propiedades** para abrir el cuadro de diálogo **Propiedades de la tabla** . En la página **FileTable** , escriba un nuevo valor para **Nombre del directorio de FileTable**.  
  
###  <a name="ReqAlter"></a>Requisitos y restricciones para modificar una FileTable  
  
-   No puede modificar el valor de **FILETABLE_COLLATE_FILENAME**.  
  
-   No puede cambiar, quitar ni deshabilitar las columnas definidas por el sistema de una FileTable.  
  
-   No puede agregar nueva columnas de usuario, columnas calculadas ni columnas calculadas persistentes a una FileTable.  
  
##  <a name="BasicsDrop"></a>Quitar una FileTable  
 Puede quitar una FileTable mediante la sintaxis normal de la instrucción [DROP TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-table-transact-sql).  
  
 Cuando se quita una FileTable, también se quitan los objetos siguientes:  
  
-   También se quitan todas las columnas de la FileTable y todos los objetos asociados con la tabla, por ejemplo, índices, restricciones y desencadenadores.  
  
-   El directorio y los subdirectorios de la FileTable que contiene desaparecen de la jerarquía de archivos y directorios de FILESTREAM de la base de datos.  
  
 Se produce un error en el comando DROP TABLE si hay identificadores de archivo abiertos en el espacio de nombres de archivo de FileTable. Para obtener información sobre cómo cerrar identificadores abiertos, vea [Administrar FileTables](manage-filetables.md).  
  
##  <a name="BasicsOtherObjects"></a>Se crean otros objetos de base de datos al crear una FileTable  
 Cuando cree una nueva FileTable, también se crean algunas restricciones y algunos índices definidos por el sistema. No puede modificar ni quitar estos objetos; desaparecen solo cuando se quita el propio objeto FileTable. Para ver la lista de estos objetos, consulte la vista de catálogo [sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql).  
  
```sql  
--View all objects for all filetables, unsorted  
SELECT * FROM sys.filetable_system_defined_objects;  
GO  
  
--View sorted list with friendly names  
SELECT OBJECT_NAME(parent_object_id) AS 'FileTable', OBJECT_NAME(object_id) AS 'System-defined Object'  
    FROM sys.filetable_system_defined_objects  
    ORDER BY FileTable, 'System-defined Object';  
GO  
```  
  
 **Índices que se crean al crear una nueva FileTable**  
 Cuando cree una nueva FileTable, también se crean los siguiente índices definidos por el sistema:  
  
|||  
|-|-|  
|**Columnas**|**Tipo de índice**|  
|[path_locator] ASC|Clave principal, no agrupada|  
|[parent_path_locator] ASC,<br /><br /> [name] ASC|Única, no agrupada|  
|[stream_id] ASC|Única, no agrupada|  
  
 **Restricciones que se crean al crear una nueva FileTable**  
 Cuando cree una nueva FileTable, también se crean las siguiente restricciones definidas por el sistema:  
  
|Restricciones|Aplica|  
|-----------------|--------------|  
|Restricciones predeterminadas en las siguiente columnas:<br /><br /> **creation_time** <br /> **is_archive** <br /> **is_directory** <br /> **is_hidden** <br /> **is_offline** <br /> **is_readonly** <br /> **is_system** <br /> **is_temporary** <br /> **last_access_time** <br /> **last_write_time** <br /> **path_locator** <br /> **stream_id**|Las restricciones predeterminadas definidas por el sistema aplican valores predeterminados a las columnas especificadas.|  
|Restricciones CHECK|Las restricciones CHECK definidas por el sistema se aplican a los siguientes requisitos:<br /><br /> Nombres de archivo válidos.<br /><br /> Atributos de archivo válidos.<br /><br /> El objeto primario debe ser un directorio.<br /><br /> La jerarquía del espacio de nombres se bloquea durante la manipulación de archivos.|  
  
 **Convención de nomenclatura para las restricciones definidas por el sistema**  
 Las restricciones definidas por el sistema descritas anteriormente se denominan con el formato ** \<constraintType\<>_ TableName>\_\<[ColumnName>\_\<] uniquifier>** donde:  
  
-   *<constraint_type>* es CK (restricción check), DF (restricción predeterminada), FK (clave externa), PK (clave principal) o UQ (restricción UNIQUE).  
  
-   uniquifier>es una cadena generada por el sistema para que el nombre sea único. * \<* Esta cadena puede contener el nombre de la FileTable y un identificador único.  
  
## <a name="see-also"></a>Consulte también  
 [Administrar FileTables](manage-filetables.md)  
  
  
