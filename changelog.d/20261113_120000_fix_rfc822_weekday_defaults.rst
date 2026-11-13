Fixed
-----

*   Fix RFC 822 date parsing when a weekday is combined with a missing
    time or timezone.

    The weekday was removed *after* the default time and timezone were
    inserted, so strings like ``Fri, 24 Nov 2023 18:28:36`` and
    ``Fri, 24 Nov 2023 +0000`` were left with too few parts and were
    silently rejected. The weekday is now removed first, and the default
    for whichever of the two is missing is then applied.

*   Emit ``feedparser.DateParseWarning`` when no date handler can parse
    a date element.

    Previously the ``*_parsed`` value was omitted with no signal at all,
    which made failures only observable downstream. The warning can be
    turned into an error or suppressed with the standard :mod:`warnings`
    machinery.
