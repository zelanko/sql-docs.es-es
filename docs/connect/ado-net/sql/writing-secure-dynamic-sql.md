---
title: Escritura de SQL dinámico seguro en SQL Server
description: Describe técnicas para escribir SQL dinámico seguro mediante procedimientos almacenados.
ms.date: 09/26/2019
ms.assetid: df5512b0-c249-40d2-82f9-f9a2ce6665bc
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: dd7b76e3333d51a94d6f215a6608511629f35fbe
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451861"
---
# <a name="writing-secure-dynamic-sql-in-sql-server"></a>Escritura de SQL dinámico seguro en SQL Server

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Descargar ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

La inyección de SQL es el proceso por el que un usuario malintencionado escribe instrucciones Transact-SQL en lugar de entradas válidas. Si la entrada se pasa directamente al servidor sin ser validada y la aplicación ejecuta accidentalmente el código inyectado, el ataque tiene la posibilidad de dañar o destruir datos.  
  
Todos los procedimientos que generan instrucciones SQL deben revisarse en busca de vulnerabilidades de inyección de código, ya que SQL Server ejecutará todas las consultas recibidas que sean válidas desde el punto de vista sintáctico. Un atacante cualificado y con determinación puede manipular incluso os datos con parámetros. Si utiliza SQL dinámico, asegúrese de parametrizar los comandos y no incluya nunca los valores de parámetro directamente en la cadena de consulta.  
  
## <a name="anatomy-of-a-sql-injection-attack"></a>Anatomía de un ataque por inyección de SQL  
El proceso de inyección consiste en finalizar prematuramente una cadena de texto y anexar un nuevo comando. Como el comando insertado puede contener cadenas adicionales que se hayan anexado al mismo antes de su ejecución, el atacante pone fin a la cadena inyectada con una marca de comentario "--". El texto situado a continuación se omite en tiempo de ejecución. Se pueden insertar varios comandos con un punto y coma (;) delimitador.  
  
Siempre y cuando el código SQL inyectado sea sintácticamente correcto, no será posible detectar alteraciones mediante programación. Por ello, debe validar todos los datos especificados por el usuario y revisar cuidadosamente el código que ejecute comandos SQL construidos en el servidor que utilice. No concatene nunca datos especificados por el usuario que no se hayan validado. La concatenación de cadenas es el punto de entrada principal de una inyección de scripts.  
  
Estas son algunas instrucciones útiles:  
  
- No cree nunca instrucciones Transact-SQL directamente a partir de datos proporcionados por el usuario; Use procedimientos almacenados para validar los datos proporcionados por el usuario.  
  
- Valide los datos especificados por el usuario mediante comprobaciones de tipo, longitud, formato e intervalo. Utilice la función Transact-SQL QUOTENAME () para escapar nombres de sistema o la función Replace () para convertir en caracteres de escape cualquier carácter de una cadena.  
  
- Implemente varias capas de validación en cada nivel de la aplicación.  
  
- Compruebe el tamaño y el tipo de los datos especificados y aplique unos límites adecuados. Esto puede impedir que se produzcan saturaciones deliberadas del búfer.  
  
- Compruebe el contenido de las variables de cadena y acepte únicamente valores esperados. Rechace las especificaciones que contengan datos binarios, secuencias de escape y caracteres de comentario.  
  
- Cuando trabaje con documentos XML, valide todos los datos con respecto a su esquema a medida que se vayan indicando.  
  
- En entornos de varios niveles, todos los datos deben validarse antes de que se admitan en la zona de confianza.  
  
- No acepte las siguientes cadenas en campos a partir de los que puedan construirse nombres de archivo: AUX, CLOCK$, COM1 a COM8, CON, CONFIG$, LPT1 a LPT8, NUL y PRN.  
  
- Utilice <xref:Microsoft.Data.SqlClient.SqlParameter> objetos con procedimientos almacenados y comandos para proporcionar comprobación de tipos y validación de longitud.  
  
- Utilice expresiones <xref:System.Text.RegularExpressions.Regex> en el código de cliente para filtrar los caracteres no válidos.  
  
## <a name="dynamic-sql-strategies"></a>Estrategias SQL dinámicas  
La ejecución de instrucciones SQL creadas dinámicamente en el código de procedimientos rompe la cadena de propiedad, lo que hace que SQL Server Compruebe los permisos del llamador con respecto a los objetos a los que tiene acceso el SQL dinámico.  
  
SQL Server tiene métodos para conceder a los usuarios acceso a los datos mediante procedimientos almacenados y funciones definidas por el usuario que ejecutan SQL dinámico.  
  
- Empleo de suplantación con la cláusula EXECUTE AS de Transact-SQL.  
  
- Firma de procedimientos almacenados con certificados.  
  
### <a name="execute-as"></a>EXECUTE AS  
La cláusula EXECUTe AS reemplaza los permisos del llamador por el del usuario especificado en la cláusula EXECUTe AS. Los procedimientos almacenados anidados o los desencadenadores se ejecutan en el contexto de seguridad del usuario proxy. Esto puede interrumpir las aplicaciones que dependen de la seguridad de nivel de fila o requieren auditorías. Algunas funciones que devuelven la identidad del usuario devuelven el usuario especificado en la cláusula EXECUTe AS, no el llamador original. El contexto de ejecución se revierte al llamador original solo después de la ejecución del procedimiento o cuando se emite una instrucción Revert.  
  
### <a name="certificate-signing"></a>Firma de certificados  
Cuando se ejecuta un procedimiento almacenado firmado con un certificado, los permisos concedidos al usuario del certificado se combinan con los del autor de la llamada. El contexto de ejecución sigue siendo el mismo. el usuario del certificado no suplanta al autor de la llamada. La firma de procedimientos almacenados requiere varios pasos para implementar. Cada vez que se modifica el procedimiento, debe volver a firmarse.  
  
### <a name="cross-database-access"></a>Acceso entre bases de datos  
El encadenamiento de propiedad entre bases de datos no funciona en los casos en que se ejecutan instrucciones SQL creadas dinámicamente. Puede resolver esto en SQL Server mediante la creación de un procedimiento almacenado que acceda a los datos de otra base de datos y la firma del procedimiento con un certificado que exista en ambas bases de datos. Esto proporciona a los usuarios acceso a los recursos de la base de datos utilizados por el procedimiento sin concederles permisos o acceso a la base de datos.  
  
## <a name="external-resources"></a>Recursos externos  
Para obtener más información, vea los recursos siguientes.  
  
|Recurso|Descripción|  
|--------------|-----------------|  
|[Procedimientos almacenados](../../../relational-databases/stored-procedures/stored-procedures-database-engine.md) e [Inyección de SQL](../../../relational-databases/security/sql-injection.md) en los Libros en pantalla de SQL Server|En los temas se describe cómo crear procedimientos almacenados y cómo funciona la inyección de SQL.|  
  
## <a name="next-steps"></a>Pasos siguientes
- [Escenarios de seguridad de aplicaciones en SQL Server](application-security-scenarios-sql-server.md)
