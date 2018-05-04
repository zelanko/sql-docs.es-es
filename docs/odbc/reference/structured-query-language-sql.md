---
title: (SQL) de lenguaje de consulta estructurado | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC]
- SQL [ODBC], about SQL
- ODBC [ODBC], SQL
ms.assetid: bebfd93e-0dc0-46b3-a531-518beb7ea976
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b3d26d6d32499d02db46762f6ce66b865a5b403c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="structured-query-language-sql"></a>Lenguaje de consulta estructurado (SQL)
Un DBMS típico permite a los usuarios almacenar, tener acceso y modificar datos en un modo organizado y eficaz. Originalmente, los usuarios de DBMS eran los programadores. Obtener acceso a los datos almacenados, es necesario escribir un programa en un lenguaje de programación, como COBOL. Mientras estos programas a menudo se escribieron para presentar una interfaz sencilla para un usuario no técnicos, acceso a los datos en sí requiere los servicios de un programador experto. No es práctico ocasional acceso a los datos.  
  
 Los usuarios no eran totalmente satisfechos con esta situación. Aunque pueden tener acceso a datos, a menudo necesario convencer a un programador DBMS para escribir un software especial. Por ejemplo, si un departamento de ventas desea ver el total de ventas del mes anterior por cada uno de sus vendedores y deseara esta información por orden de clasificación por la longitud de cada vendedor de servicio en la empresa, que tenía dos opciones: ya sea un programa ya existía que permite la información que se va a tener acceso exactamente de esta manera, o el departamento tuvo que pide a un programador escribir este tipo de programa. En muchos casos, esta era más trabajo que fue que vale la pena, y siempre es una solución costosa para las consultas de un solo uso o ad hoc. Como cada vez más usuarios deseaban de fácil acceso, este problema ha crecido más grandes y más grandes.  
  
 Permitir a los usuarios tener acceso a datos de manera ad hoc necesario darles un idioma en el que expresar sus solicitudes. Una única solicitud para una base de datos se define como una consulta; Este tipo de lenguaje se denomina un lenguaje de consulta. Muchos lenguajes de consulta se desarrollaron para este propósito, pero uno de estos pasara a ser más populares: lenguaje de consulta estructurado, inventado en IBM en la década de 1970. Lo más comúnmente se conoce por su acrónimo, SQL y se pronuncia como "ess-indicación-ell" y como "sequel"; Este manual usa la pronunciación anterior. SQL se convirtió en un estándar en 1986 ANSI y una imagen ISO estándar en 1987; hoy en día se usa en una gran muchos sistemas de administración de base de datos.  
  
 Aunque SQL resuelve las necesidades ad hoc de los usuarios, no desaparecer la necesidad de acceso a los datos por los programas informáticos. De hecho, la mayoría de base de datos acceso aún era (y es) programas de entrada de datos mediante programación, en forma de informes programados periódicamente y análisis estadísticos, como los utilizados para entrada de pedido y los datos de programas de manipulación, como las que se usan para conciliar las cuentas de y generar órdenes de trabajo.  
  
 Estos programas también utilizan SQL, con una de las tres técnicas siguientes:  
  
-   **SQL incrustadas**, en qué SQL instrucciones se incrustan en un lenguaje de host como C o COBOL.  
  
-   **Los módulos SQL**, en qué instrucciones SQL se compilan en el DBMS y se le llama desde un lenguaje host.  
  
-   **Interfaz de nivel de llamada**, o CLI, que consta de las funciones llamadas para pasar instrucciones SQL en el DBMS y recuperar resultados de lo DBMS.  
  
> [!NOTE]  
>  Es un accidente histórico que el término se utiliza la interfaz de nivel de llamada en lugar de programación de aplicaciones (API), la interfaz otro término para lo mismo. En el mundo de la base de datos, la API se usa para describir SQL propia: SQL es la API para un DBMS.  
  
 De estas opciones, SQL incrustado es el uso más frecuente, aunque la mayoría de los DBMS principales admite CLI de propietarias.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Procesar una instrucción SQL](../../odbc/reference/processing-a-sql-statement.md)  
  
-   [SQL incrustado](../../odbc/reference/embedded-sql.md)  
  
-   [Módulos SQL](../../odbc/reference/sql-modules.md)  
  
-   [Interfaces de nivel de llamada](../../odbc/reference/call-level-interfaces.md)
