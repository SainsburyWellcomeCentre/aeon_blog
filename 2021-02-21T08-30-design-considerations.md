---

---

# Design Considerations

Datasets collected in Project Aeon differ from traditional experimental research in systems neuroscience in unique ways, creating both challenges and opportunities for data exploration, visualization and analysis. Here we outline and discuss these challenges and opportunities in comparison with recently emerging trends in large-scale distributed database management systems.

## The goal

Studying the brain and behaviour in natural settings has always been severely constrained by the sheer number of variables and scales involved. In response, experimenters invariably attempt to constrain behaviour to a manageable scale by studying a few changing variables at a time, while aiming to keep every other factor fixed.

To do this, behavioural assays often involve reproducible conditions where sequences of stimuli, and the possible responses of animals to those stimuli, is limited and precisely controlled. To ensure robustness to variability in any uncontrolled variables, these conditions are then repeated thousands of times, across multiple animals. This naturally induces a task-centric or experiment-centric description of the brain and behaviour, where datasets are separated from the outset into subjects, sessions and trials, stimulus-response logs, decisions, outcomes, etc.

One of the conceptual aims of Project Aeon is to move the field gradually towards an alternative approach: can we understand new relationships in freely moving behaviour data by allowing animals to set their own goals and control their own behaviour in the environment, and systematically measuring as much as we can from that rich multi-dimensional space of interactions?

Crucially, we are assuming that many variables of interest in our experiments will be a priori hidden from us, and not made explicit by any kind of trial structure, which means relationships will have to be discovered, rather than directly measured, from high-volume data.

# Data Schemas

In task-centric approaches to the study of behaviour, the relationships between different kinds of experimental data can often be reasonably defined before data collection begins, by taking into account the constraints of the experimental protocol, the apparatus, and expected outcomes and measurements of interest.

In relational database design practice this is called a database schema: a specification outlining the structure of the data stored in the database, and the relationships between them. These schemas might reflect the natural organization of an experiment, for example we might define that there are tables of subjects, which are related to tables of experimental sessions, and tables of trials which store outcomes of fixed experimental conditions. Such schemas are critical in most databases to guarantee efficient access to the data, and their specification is often required *prior* to the insertion (a.k.a. ingestion) of data in the database. Because of the intimate relationship between schemas and database structure, changing the schema might require drastic changes to the underlying data store, or even purging and recreation of the entire database.

As discussed above, however, Project Aeon experiments are set up in a way that no such separation of the experiment in subjects, sessions and trials really exists. Instead, the assay provides opportunities for animals to express many different possible natural relationships between themselves, objects in the world, and other animals, all monitored in continuous fashion. Indeed, we could say that with Project Aeon the aim is to allow for experimenters to *discover* the schemas implicit in animal behaviour, by exploring the data, rather than imposing a schema beforehand and measuring many occurrences in fixed data tables.

## Primary Schemas

That said, we do have primary schemas, which will constrain how the raw data is stored in the first place. These schemas will be organized mostly around the measurement and control devices in the Project Aeon arena, which due to the specific characteristics of our data acquisition systems, allow every measurement to be uniquely timestamped in a common temporal reference frame with microsecond precision.

The spatial location of each measuring sensor will also be precisely determined, either by mechanical constraint, or by precise spatial calibration procedures. Taken together, this means every raw data point can be assigned a spatial and temporal stamp which can be related to the spatial and temporal stamps of every other measurement in the arena.

All data in Project Aeon will be recorded according to this common spatiotemporal schema, which will form the backbone of a unified framework for exploring and discovering behaviour relationships across space and time.

## Feature Extraction

Several features of interest which will be used to model behavioural relationships in Project Aeon will need to be extracted a posteriori from the raw data. Some of them might be advantageous to precompute and cache for the entire temporal timeseries (e.g. individual animal trajectories), while others might be lightweight and constrained enough as to be computed during query evaluation (e.g. peri-event time histograms), or relative to certain spatial frames of reference (e.g. position of one animal relative to another animal). Below we outline some examples of feature extraction and preprocessing which are likely to come up during Project Aeon.

### Trajectory Data

Spatio-temporal trajectory data for individual animals needs to be extracted from raw video recorded across different imaging devices installed around the arena. Individual frames will be triggered simultaneously, so identified spatial locations can be assigned a unique timestamp across all devices. However, computer vision preprocessing will be required to correctly identify and track animal identities across the video. Tracking data may have to be combined with other sensor data such as RFID readings to ensure the correct animal identity is assigned throughout the entire experiment.

Individual cameras will be calibrated so that their field-of-view, position, and orientation relative to the arena reference frame is known. The goal is to allow triangulation of a tracked animal position in 3D space. Conversely, once the 3D position of an object of interest is known accurately, its projection on any other calibrated image sensor can be determined, allowing us to choose different viewpoints or close-ups into a behaviour.

Computer vision preprocessing is a compute-heavy task, especially across multiple video devices, so there is a clear advantage to caching the results of such preprocessing for subsequent queries. Depending on algorithmic complexity, it might even be desirable to compute certain processing steps online during the acquisition stage, such as unlabeled trajectory data.

### Spike Times

## Data Ingestion

How high is high-volume data in Project Aeon? For our first behavioural arena we anticipate anywhere between 3 to 5 behavioural imaging devices, around 10 behaviour patches and  acquisition sensors

# Cluster Computing

## Timeseries Data



### Dense and Sparse Timeseries

## Spatial Data

### Spatial Hashing

Once 

[Geohashing](https://en.wikipedia.org/wiki/Geohash)

## Spatiotemporal Data

# Data Provenance

To effectively enable and organize massive parallel exploration and discovery in Project Aeon datasets, we adopt a strict policy to data generation and storage. Specifically, every data element in Project Aeon belongs to only one of two classes: *raw data* or *derived data*.

Raw data are the result of experiments or manual input, and never change from the moment they are generated. Derived data are artifacts computed deterministically from the raw data. They are defined entirely by computational procedures working on the raw data.

### Raw Data

Raw data are the primary artifacts of experimental measurements in Project Aeon. Once raw data is acquired and timestamped, it becomes immutable. This means we will never update or revise these values, or update their timestamps, ever again. This assumption of immutable timestamped data introduces several immediate advantages to data processing pipelines:

  * **Parallel access:** since raw data is guaranteed to be immutable, every file in the dataset can be accessed simultaneously by an arbitrary number of clients, ensuring consistency without the need of locking access to files;
  * **Caching:** derived measurements, statistics, or conclusions deterministically computed from immutable raw data will also never change, which means they can be cached indefinitely;
  * **Total Ordering:** since every raw data element is timestamped in a common temporal reference frame, there is a natural total ordering imposed on Project Aeon datasets. This can be exploited for fast indexing and partitioning of temporal data.

### Derived Data

Derived data are artifacts computed from the raw data by deterministic computational procedures, or code. Because of the immutability of raw data, this means that by storing the source code which generates the derived data together with the original source of raw data, we will always be able to reconstruct the derived artifacts through computation.

If the source code for all derived data computations is uniquely tagged and version-controlled, we can safely pipe derived data as input to other computations, as a list of dependencies. These assumptions on derived data introduce several immediate advantages to data exploration and analysis pipelines:

  * **Storage efficiency:** because code is so incredibly compact, and version-controlling the code is enough to completely specify the derived data, we can safely delete any intermediate artifacts we are no longer interested in and keep only the code;
  * **Reproducibility:** since all derived artifacts can be deterministically reconstructed from raw data and code, this means every analysis step required to generate Project Aeon outputs will be reproducible;
  * **Provenance:** since every derived artifact will store a reference to the data dependencies it requires (both raw and derived data), we can always reconstruct and track the exact history of how a certain artifact was generated.

## Challenges and Questions

Despite the simplicity of the assumptions above, there are several situations in which we feel these constraints might be violated. Below we outline some of these situations, and how to address them to preserve the conceptual integrity of the Project Aeon data provenance scheme.

### Accidental Mutation

In order to guarantee the immutability of experimental raw data against accidental mutations, we will limit write access on the data store to the acquisition computer. Every other human and machine user will have only read access to the data in bulk storage. Tape backup of acquired data will be performed in incremental fashion to provide an extra level of protection.

Source code for derived data computations will be stored using a distributed version-control system such as Git. Automatic validations will be in place to ensure no missing dependencies are missing or incorrect. In any case, since all operations on the raw data are non-destructive, the state of data preprocessing pipelines can always be reverted and corrected afterwards. History on the main branch of the repository *must not* be rewritten to ensure the provenance of derived artifacts, so the use of branches for developmental experimentation should be encouraged and possibly strictly enforced.

### Manual Analysis Steps

There might be situations in which specific analysis steps cannot be fully automated through code scripts, for example during manual annotation of data by human operators. This would violate the reproducibility constraints for derived data since we cannot reliably reproduce the human decision making process during manual annotation.

We can, however, log the annotation procedure itself and treat it as an experiment. Essentially we keep a complete record of the decisions the operator made while preprocessing the data. For example, if ROIs need to be selected, or frames labelled, we would simply need to store the frame numbers or ROI coordinates which the human provided to the annotation pipeline.

In other words, manual annotation steps are treated exactly the same as raw data, to be timestamped and stored as an immutable data store for future analysis steps. Such procedures should also record enough documentation, metadata and rely on open-source reproducible tools to allow future human operators to repeat the procedure, if further manual annotation is to be performed. For avoidance of doubt, refinement of a manual annotation is possible, but will itself generate a new timestamped immutable dataset.

In order to keep with the principles of efficient storage and data provenance, manual annotation tools which avoid direct editing or duplication of raw input files should be preferred. As an example, manual editing of a picture using a bitmap image editor would be vastly inefficient as we would have to store an expensive binary copy of the manipulated image. Rather, we should strive to store only the human provided directives themselves, such as the coordinates of selected ROIs, key strokes, text labels and the like which can be logged with minimal effort and reliably applied to reconstruct the manual annotation process. For example, we might prefer tools supporting the execution of macros or scripts from batch, as they are more likely to allow the ability to reconstruct the output of the manual processing steps from data.
