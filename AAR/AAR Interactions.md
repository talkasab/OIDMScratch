# Interactions in Assisted Reporting

- **Form definition**: Advisor sends a command with a simple definition of some questions (specified in JSON structure, with schema similar to the current CAR/DS/Clinical Guidance) along with an identifier for the answer. PowerScribe gets the answer from the user and puts the value back into the DCOM[^1] with that label, and the advisor sees the answer and goes ahead.

- **Image Map**: Allow for a relatively complex image map which either directly pops up for the user (or which the user is invited to with a button), but interaction is otherwise similar to **Form Definition**.

- **Adaptive Cards**: Same as above, but instead of defining the form/interaction using the CAR/DS/Clinical Guidance, the Advisor specifies the interaction using [Adaptive Cards](https://adaptivecards.io). Again, the Advisor gives an identifier for the answer, and after PowerScribe instantiates the Card and gets data back, it puts the answering JSON data into the DCOM tagged with that identifier.

- **External Web App**:
  - Developer creates a single-page application (SPA; possibly using a standard framework like React) which implements the dynamic interaction with the user the developer desires. The SPA accepts a bolus of JSON data as an initial state. The SPA should be able to determine when the user has answer satisfactorily and set the output data to a "response" element in the DOM and sets a flag on a "done" element. The SPA can be assigned a standard identifier place, and the identifier put into the Advisor's configuration file
  - When Advisor wants to trigger the interaction, it creates a bolus of state data from the DCOM and sends a command to open the SPA (specified by the identifier) with that data as the initial state and an identifier .
  - PowerScribe maps the SPA ID to the URL where it actually lives and opens the SPA with the initial state, and monitors the SPA for the "done" flag to be set. When the flag is set by the SPA, it pulls the response data out of the "response" element and closes the SPA window. It then injects the reponse data into the DCOM tagged with the identifier.
  - _As an added layer, could the SPA could update the "response" data before setting the "done" flag; PowerScribe could put the data in the DCOM and the script could see it. Could the script then send more data back to the SPA, asking PowerScribe to inject the data into the SPA's DOM somewhere standard?_

> NB: Need to figure out what happens if the advisor gets run
> again after it has sent the request for information but before
> the answer gets back.
>
> NB: Also need to be able to deal gracefully
> with a timeout situation where the user never answers; maybe
> before the user answers, have the identifier with a value like
> "Waiting since 2023-02-15T12:34:12Z".

[^1]: Data Context Object Model
