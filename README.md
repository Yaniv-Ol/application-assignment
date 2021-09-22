**Drug administration producer-consumer assignment**

**Problems:**

Drug administration even occurs upon actually administrating the drug. There is no feedback or control on the drug administration:
For example let’s assume that a certain drug was administered but for some reason it was not yet registered via the consumer (i.e. big queue, problem updating the DB, service failure, queue failure failure…)
Someone may access the API and there will be no mention of the last drug administration so he/she may administer another dose and may cause over dose.

**Solutions:**

1.	Setting drug administration will be transactional so that the actual dose will be administered only after successful updating of the DB - rolled back in case of failure.
2.	The actual administrating of a dose will be queried on a log/cache on the publisher prior to dosing the patient and the consumer will only save the data and will not be mission critical element
3.	An overseer: A third service that will check that both services are in sync and will not allow administrating a dose prior to the data being successfully saved to the DB – my least favorite option (added complexity, another point of failure)

This is not exactly what you requested but it is the work of an architect and not an engineer.
I hope it will suffice.

Yaniv Olchovsky.


