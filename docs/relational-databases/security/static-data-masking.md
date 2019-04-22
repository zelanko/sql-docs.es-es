---
title: Enmascaramiento estático de datos | Microsoft Docs
ms.date: 04/10/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: a62f4ff9-2953-42ca-b7d8-1f8f527c4d66
author: aliceku
ms.author: aliceku
manager: ajayj
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 91b0fde06d400b2c519e9e6c86854197a2aecd13
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59516471"
---
# <a name="static-data-masking"></a>Enmascaramiento estático de datos
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Enmascaramiento estático de datos se ha publicado como un componente de [SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md) 18.0 versión preliminar 5 y versiones posteriores. Hemos decidido que nuestro prototipo actual no cumple con las expectativas de nuestros clientes. Por lo tanto, no llevaremos adelante esta capacidad. Le informaremos sobre nuestros planes si tenemos un candidato de reemplazo.

![Enmascaramiento de datos estático](../../relational-databases/security/media/sql-static-data-masking/static_data_masking_intro_image.PNG)


## <a name="what-is-static-data-masking"></a>¿Qué es el enmascaramiento estático de datos? 
Enmascaramiento estático de datos es una característica de SQL Server Management Studio que permite a los usuarios crear una copia enmascarada de una base de datos. La característica se desarrolló para las organizaciones que necesitan compartir datos, algunos de ellos confidenciales, entre equipos o con otras organizaciones. 

Al reemplazar los datos confidenciales (datos anteriores al enmascaramiento) con datos nuevos (datos posteriores al enmascaramiento), el enmascaramiento estático de datos facilitará los escenarios siguientes: 
- Desarrollo y pruebas 
- Análisis e informes empresariales 
- Solucionar problemas 
- Uso compartido de la base de datos con un consultor, un equipo de investigación o terceros 

En el ejemplo siguiente se muestra cómo funciona el enmascaramiento estático de datos. Antes del enmascaramiento, la columna contiene números del seguro social. Después del enmascaramiento, los cinco primeros dígitos de cada número del seguro social se han reemplazado por números generados aleatoriamente.

| Número del seguro social de EE. UU. (antes del enmascaramiento)   | Número del seguro social de EE. UU. (después del enmascaramiento)  |
| ------------- | ------------- |
| 140-38-9110 | 302-92-9110 |
| 463-34-5535 | 189-70-5535 |
| 116-30-8733 | 201-01-8733 |
| 209-36-1971 | 683-10-1971 |
| 372-38-6948 | 372-38-6948 |
| 267-64-2334 | 100-03-2334 |
| 523-93-4176 | 582-20-4176 |
| 573-91-5137 | 730-20-5137 |
| 612-72-1026 | 369-40-1026 |

Los usuarios de enmascaramiento estático de datos pueden elegir entre varias funciones de enmascaramiento. Según la función de enmascaramiento, los datos anteriores y posteriores al enmascaramiento pueden estar estrechamente relacionados o no tener ninguna relación. Una función de enmascaramiento que realice un orden aleatorio generará datos posteriores al enmascaramiento estrechamente relacionados con los datos anteriores al enmascaramiento. 

| Número del seguro social de EE. UU. (antes del enmascaramiento) | Número del seguro social de EE. UU. (después del enmascaramiento) |
| ------------- | ------------- |
| 140-38-9110 | 612-72-1026 |  
| 463-34-5535 | 372-38-6948 | 
| 116-30-8733 | 523-93-4176 |
| 209-36-1971 | 209-36-1971 | 
| 372-38-6948 | 140-38-9110 |
| 267-64-2334 | 463-34-5535 | 
| 523-93-4176 | 573-91-5137 | 
| 573-91-5137 | 267-64-2334 | 
| 612-72-1026 | 116-30-8733 |

Una función de enmascaramiento que realice una sustitución con un valor NULL generará datos posteriores al enmascaramiento sin relación con los datos anteriores al enmascaramiento. 
 
| Número del seguro social de EE. UU. (antes del enmascaramiento) | Número del seguro social de EE. UU. (después del enmascaramiento) |
| ------------- | ------------- |
| 140-38-9110 | NULL |  
| 463-34-5535 | NULL | 
| 116-30-8733 | NULL |
| 209-36-1971 | NULL | 
| 372-38-6948 | NULL |
| 267-64-2334 | NULL | 
| 523-93-4176 | NULL | 
| 573-91-5137 | NULL | 
| 612-72-1026 | NULL |

## <a name="how-does-static-data-masking-work"></a>¿Cómo funciona el enmascaramiento estático de datos?
El enmascaramiento estático de datos funciona en el nivel de columna. Los usuarios seleccionan las columnas que quieren enmascarar y, para cada columna seleccionada, la función de enmascaramiento que quieren aplicar. Existen varias funciones de enmascaramiento entre las que elegir. Se describen en detalle en [Funciones de enmascaramiento](#masking-functions). 

Después, el enmascaramiento estático de datos creará una copia de la base de datos. Para Azure SQL Database, la copia se realiza a través de la [función de copia](https://azure.microsoft.com/blog/static-data-masking-preview/). Para SQL Server, se realiza a través de una operación de copia de seguridad seguida de una operación de restauración. A partir de ahí, para cada columna, el enmascaramiento estático de datos empieza a sustituir los datos anteriores al enmascaramiento con datos posteriores al enmascaramiento según la función de enmascaramiento seleccionada. 

El reemplazo se realiza en el nivel de almacenamiento. Como resultado, no es posible recuperar los datos anteriores al enmascaramiento de la copia enmascarada de la base de datos después de que se haya completado el enmascaramiento estático de datos.

## <a name="how-to-guide"></a>Guía de procedimientos

A continuación se muestra una guía paso a paso para ejecutar el enmascaramiento estático de datos. 
 
1. Inicie SQL Server Management Studio. Conéctese a la base de datos. En el panel **Explorador de objetos** en el lado izquierdo, expanda la carpeta Bases de datos. Haga clic con el botón derecho en la base de datos que quiera enmascarar. Haga clic en **Tareas**. Haga clic en **Enmascarar base de datos... (versión preliminar)**.
 
 ![Menú Tareas](../../relational-databases/security/media/sql-static-data-masking/task_data_masking.PNG)
 
2. Se abrirá la ventana de configuración de enmascaramiento. Se mostrarán todas las tablas de la base de datos. Las tablas se presentan por esquema y, después, se ordenan por orden alfabético dentro de un esquema. 
 
 ![Interfaz de usuario](../../relational-databases/security/media/sql-static-data-masking/ui_dropdown.PNG)
 
3. Haga clic en el icono desplegable situado junto al nombre de la tabla para obtener una lista de todas las columnas de la tabla. Para cada columna en la tabla, se especifica el tipo de datos de la columna, y también si la columna acepta valores NULL. Una columna que acepta valores NULL es una columna que puede recibir el valor NULL como una entrada. 
 
 ![Lista desplegable de la tabla](../../relational-databases/security/media/sql-static-data-masking/ui_dropdown_column.png)
 
4. Seleccione todas las columnas que quiera enmascarar y la función de enmascaramiento que quiera aplicar. Los tipos de enmascaramiento disponibles son **Shuffle** (Orden aleatorio), **Group Shuffle** (Orden aleatorio de grupo), **Single value** (Valor único), **NULL** y **String Composite** (Composición de cadena). 
 
 ![Lista desplegable de funciones de enmascaramiento](../../relational-databases/security/media/sql-static-data-masking/masking_functions.PNG)
 
 NOTA: La mayoría de estas funciones de enmascaramiento tienen parámetros de configuración adicionales. Para el enmascaramiento de orden aleatorio, Enmascaramiento estático de datos proporciona un parámetro predeterminado. Para el enmascaramiento de tipo Orden aleatorio de grupo, Valor único y Composición de cadena, el usuario debe proporcionar parámetros de configuración. Para cambiar o proporcionar parámetros de configuración, haga clic en la opción **Configurar...**  y especifique un valor (alternativo) para el parámetro en el cuadro de diálogo que aparece. En [Funciones de enmascaramiento](#masking-functions) se proporcionan descripciones detalladas de cada función de enmascaramiento.
 
 ![Botón de configuración de las funciones de enmascaramiento](../../relational-databases/security/media/sql-static-data-masking/masking_functions_configure.png)
 
 Las opciones de configuración de enmascaramiento se validan para los errores y advertencias relacionados con el esquema y la configuración sobre la marcha.  Todo lo que se detecte se mostrará como un icono a la izquierda sobre el que se puede mantener el mouse para obtener detalles adicionales. 
 
 En el ejemplo siguiente, el usuario ha seleccionado el enmascaramiento NULL para una columna que no permite valores NULL (restricción NOT NULL).
 
 ![Error del mecanismo de validación](../../relational-databases/security/media/sql-static-data-masking/validation_mechanism_error_message.PNG)
 
 En el ejemplo siguiente, el usuario ha seleccionado el enmascaramiento de orden aleatorio de grupo para una única columna. Como Orden aleatorio de grupo requería un mínimo de dos columnas, se ha emitido una advertencia. 
 
 ![Advertencia del mecanismo de validación](../../relational-databases/security/media/sql-static-data-masking/validation_warning.PNG)
 
5. La configuración de enmascaramiento completa se puede guardar en un archivo XML para su uso posterior.  Aunque la configuración de la función de enmascaramiento es idéntica entre las bases de datos de Azure SQL y las bases de datos locales, hay algunas pequeñas diferencias sobre qué propiedades adicionales (por ejemplo, la ruta de acceso del archivo de copia de seguridad) se guardan. Para guardar la configuración, haga clic en **Guardar configuración**, proporcione un nombre de archivo y haga clic en Guardar.  Después, los usuarios pueden cargar un archivo de configuración existente mediante **Cargar configuración**. Se recomienda usar archivos de configuración para las tablas con un gran número de columnas. 
 
 ![Archivo de configuración](../../relational-databases/security/media/sql-static-data-masking/load_save_config.PNG)
 
6. Enmascaramiento estático de datos creará una carpeta en la carpeta **Documentos** del usuario denominada Enmascaramiento estático de datos y colocará archivos de registro en su interior. Los archivos de registro pueden ser útiles con fines de depuración. El nombre del archivo de registro se indica en la parte inferior de la ventana de configuración. 
  
 
7. (Solo SQL Server) Si usa Enmascaramiento estático de datos en una base de datos local, realizará una operación de copia de seguridad y restauración. En el **Paso 2: Clonar la ubicación del archivo .BAK**, proporcione la ubicación en el servidor donde se va a almacenar el archivo de copia de seguridad. 

## <a name="masking-functions"></a>Función de enmascaramiento

### <a name="null-masking"></a>Enmascaramiento NULL

El enmascaramiento NULL reemplaza todos los valores de la columna con el valor NULL. Si la columna no admite valores NULL, la herramienta Enmascaramiento estático de datos devolverá un error. 

### <a name="single-value-masking"></a>Enmascaramiento de un solo valor

El enmascaramiento de un solo valor reemplaza todos los valores de la columna con un único valor fijo, especificado por el usuario. El formato de la entrada debe ser convertible al tipo que tenga la columna seleccionada. Para especificar el valor, haga clic en **Configurar...**, proporcione un valor y después haga clic en **Aceptar**. 

![Parámetro de enmascaramiento de un solo valor](../../relational-databases/security/media/sql-static-data-masking/single_value_parameter.PNG)


### <a name="shuffle-masking"></a>Enmascaramiento de orden aleatorio

Todos los valores de la columna se ordenan aleatoriamente en filas nuevas. No se generan datos nuevos. El enmascaramiento de orden aleatorio proporciona la opción de mantener las entradas NULL en la columna. Para ello, haga clic en **Configurar...** y active la casilla Maintain NULL positions (Mantener posiciones NULL).

![Parámetro de enmascaramiento de orden aleatorio](../../relational-databases/security/media/sql-static-data-masking/shuffle_parameter.PNG)

A continuación se muestra un ejemplo de enmascaramiento aleatorio sin mantener los valores NULL y, después, con los valores mantenidos.


| Número del seguro social de EE. UU. (antes del enmascaramiento) | Número del seguro social de EE. UU. (después del enmascaramiento con entradas NULL aleatorias) | Número del seguro social de EE. UU. (después del enmascaramiento con entradas NULL no aleatorias) |
| ------------- | ------------- | ------------- |
| 116-30-8733 | 612-72-1026 | 463-34-5535 |
| 140-38-9110 | NULL | 573-91-5137  |
| 209-36-1971 | 523-93-4176 | 140-38-9110 |
| NULL | 209-36-1971 | NULL |
| 463-34-5535 | 140-38-9110 | 116-30-8733  |
| 523-93-4176 | 463-34-5535 | 612-72-1026  |
| NULL | 573-91-5137 | NULL |
| 573-91-5137 | NULL | 523-93-4176 |
| 612-72-1026  | 116-30-8733  | 209-36-1971 |  

### <a name="group-shuffle-masking"></a>Enmascaramiento de orden aleatorio de grupo
Orden aleatorio de grupo enlaza varias columnas en un grupo de orden aleatorio. Las columnas de un grupo de orden aleatorio se mezclarán juntas. El usuario debe especificar el nombre del grupo de orden aleatorio mediante la opción **Configurar...**.

![Parámetro de enmascaramiento de orden aleatorio de grupo](../../relational-databases/security/media/sql-static-data-masking/group_shuffle_parameter.PNG)

El orden aleatorio de grupo se produce dentro de la misma tabla; si se usa el mismo nombre de grupo de orden aleatorio en varias tablas, los dos órdenes aleatorios de grupo son acciones independientes. El nombre del grupo debe ser el mismo para todas las columnas que se incluyan en el grupo. El nombre distingue mayúsculas de minúsculas. Puede haber varios grupos de orden aleatorio (con nombres diferentes) en la misma tabla. 

### <a name="string-composite-masking"></a>Enmascaramiento de composición de cadena

El enmascaramiento de composición de cadena genera cadenas aleatorias según un patrón. Está diseñado para las cadenas que deben seguir un patrón predefinido para que sean una entrada válida. Por ejemplo, los números del seguro social estadounidense tienen el formato 123-45-6789. La sintaxis para el enmascaramiento de composición de cadena se especifica en el cuadro de diálogo donde el usuario tiene que escribir el patrón.

![Parámetro de enmascaramiento de composición de cadena](../../relational-databases/security/media/sql-static-data-masking/string_composite.PNG)

El enmascaramiento de composición de cadena proporciona tres patrones de ejemplo que se pueden probar si se hace clic en ellos. Si hace clic en Número de teléfono, el cuadro de patrón se rellenará automáticamente con la fórmula necesaria para generar números de teléfono estadounidenses aleatorios.

![Ejemplo de parámetro de enmascaramiento de composición de cadena](../../relational-databases/security/media/sql-static-data-masking/string_composite_phone_example.PNG)

El enmascaramiento de composición de cadena también tiene un modo avanzado que permite reemplazar subsecciones de los datos existentes por las cadenas generadas por el patrón. La parte reemplazada de la cadena se determina mediante el grupo de capturas en una expresión regular. Por ejemplo, se puede reemplazar la parte del nombre de usuario de un correo electrónico al tiempo que se conserva el dominio, o bien se puede reemplazar un número de teléfono y conservar el código de área. [Aquí](https://docs.microsoft.com/dotnet/standard/base-types/regular-expression-language-quick-reference) encontrará más información sobre las expresiones regulares.

![Ejemplo avanzado de parámetro de enmascaramiento de composición de cadena](../../relational-databases/security/media/sql-static-data-masking/string_composite_advanced.PNG)

El enmascaramiento de composición de cadena y su modo avanzado solo se pueden usar para las columnas con los [tipos de datos](../../t-sql/data-types/data-types-transact-sql.md) char, varchar, text, nchar, nvarchar y ntext.

## <a name="limitations"></a>Limitaciones 

El enmascaramiento estático de datos tiene las limitaciones siguientes:

- El enmascaramiento estático de datos no admite bases de datos con [tablas temporales](../../relational-databases/tables/temporal-tables.md).

- El enmascaramiento estático de datos no enmascara tablas [optimizadas para memoria](../../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md).

- El enmascaramiento estático de datos no enmascara [columnas calculadas](../../relational-databases/tables/specify-computed-columns-in-a-table.md) y columnas de [identidad](../../t-sql/statements/create-table-transact-sql-identity-property.md).

- El enmascaramiento estático de datos no admite bases de datos de hiperescalado de Azure SQL.

- El enmascaramiento estático de datos no es compatible con los tipos de datos Geometry y Geography. 

Además, el enmascaramiento estático de datos presenta tres limitaciones en sus capacidades de enmascaramiento:

- El enmascaramiento estático de datos no actualiza las [estadísticas del histograma](../../relational-databases/statistics/statistics.md). Por tanto, la copia enmascarada de la base de datos todavía puede contener datos confidenciales en las estadísticas del histograma una vez que se haya completado el enmascaramiento estático de datos. Considere la posibilidad de ejecutar [UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md) para solucionar este problema. 

- Si el enmascaramiento estático de datos devuelve un error, se suspenden todas las operaciones de enmascaramiento. La copia de la base de datos no se elimina y puede contener información confidencial. El usuario es responsable de eliminar la copia de la base de datos si el enmascaramiento estático de datos devuelve un error. 

- (Solo SQL Server) El [archivos de datos](../../relational-databases/databases/database-files-and-filegroups.md) y el [archivo de registro](../../relational-databases/logs/the-transaction-log-sql-server.md) todavía pueden contener fragmentos de datos confidenciales en la memoria sin asignar después de que se haya completado el enmascaramiento estático de datos. Estos datos confidenciales se pueden recuperar con un editor hexadecimal si le concede acceso a los archivos de datos y el archivo de registro.

## <a name="see-also"></a>Consulte también  
 [Enmascaramiento dinámico de datos](../../relational-databases/security/dynamic-data-masking.md)   
 [Introducción al Enmascaramiento dinámico de datos de SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-static-data-masking-get-started/)  
