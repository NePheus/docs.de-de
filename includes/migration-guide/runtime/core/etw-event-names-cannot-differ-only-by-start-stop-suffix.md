### <a name="etw-event-names-cannot-differ-only-by-a-start-or-stop-suffix"></a>ETW-Ereignisnamen können sich nicht nur durch das Suffix „Start“ oder „Stop“ unterscheiden

|   |   |
|---|---|
|Details|In .NET Framework 4.6 und 4.6.1 löst die Laufzeit <xref:System.ArgumentException> aus, wenn zwei Ereignisnamen der Ereignisablaufverfolgung für Windows (ETW) sich lediglich durch das Suffix &quot;Start&quot; oder &quot;Stop&quot; unterscheiden (z.B. wenn ein Ereignis mit <code>LogUser</code> benannt ist und das andere mit <code>LogUserStart</code>). In diesem Fall kann die Runtime die Ereignisquelle nicht erstellen, die dann keine Protokollierung durchführen kann.<ul><li>[X ] Quirking // Verwendet einen Mechanismus, um das Feature zu aktivieren oder zu deaktivieren, und verwendet normalerweise Laufzeitziel, AppContext oder config-Dateien. Muss in einigen Situationen automatisch aktiviert werden.</li><li>[] Unterbrechung zur Buildzeit / / Löst bei einem erneuten Kompilierversuch eine Unterbrechung aus</li></ul>|
|Vorschlag|Stellen Sie sicher, dass zwei Ereignisnamen sich nicht nur durch das Suffix &quot;Start&quot; oder &quot;Stop&quot; unterscheiden, um die Ausnahme zu verhindern. Diese Anforderung wird mit .NET Framework 4.6.2 entfernt. Die Laufzeit kann Ereignisnamen unterscheiden, die sich nur durch das Suffix &quot;Start&quot; oder &quot;Stop&quot; unterscheiden.|
|Bereich|Microsoft Edge|
|Version|4.6|
|Typ|Laufzeit|

