Query to JSON
Convert the user's query into JSON matching the given schema.

Inputs
Schema: from the user's message, an attached file, or skill args. If none is given, ask for it once before proceeding.
Query: the text to convert.
Rules
Output only the JSON object, no prose, no code-fence commentary, no reasoning.
Use only keys defined in the schema. Never add extra keys.
Respect types, enums, formats, min/max and required fields exactly.
Extract values only from the query. Never invent data.
Missing optional field: use null (or omit if the schema forbids null).
Missing required field: use the schema default if one exists; otherwise ask the user for it.
Normalize values to the schema's format (dates as ISO 8601, numbers as numbers, booleans as true/false, enums matched case-exactly).
Ambiguous query: pick the most literal reading; mention the ambiguity only if it changes a required field.
Check before returning
Valid JSON that parses.
Every required field present.
Every value passes its type/enum constraint.
Example
Schema: {"intent": "enum[search,book,cancel]", "city": "string|null", "date": "date|null"} Query: "Book me something in Muscat for 3 Nov 2026" Output: {"intent":"book","city":"Muscat","date":"2026-11-03"}
