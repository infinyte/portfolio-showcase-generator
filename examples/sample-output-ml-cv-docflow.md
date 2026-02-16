# Portfolio Showcase: DocFlow

## Quick Reference
- **Tech Stack**: .NET 8.0, C#, OpenCV, PyTorch/ONNX, Tesseract OCR, Roslyn, Genetic Algorithms
- **Duration**: Side project (ongoing)
- **Role**: Sole Developer, Architect, ML Engineer
- **Impact**: Whiteboard photo → working code in seconds, 91+ tests passing, full pipeline operational

---

## 1. Executive Summary

Built DocFlow, an open-source AI-powered documentation toolkit that transforms whiteboard photos into working code through computer vision and machine learning. Designed and implemented a complete pipeline combining OpenCV image preprocessing, custom OCR for handwriting recognition, and genetic algorithm-based layout optimization to extract diagrams from messy whiteboard photos and generate compilable C# code with DDD patterns. Achieved full bidirectional transformation between C# and Mermaid diagrams with 91+ passing tests, demonstrating both computer vision expertise (M.S. focus area) and enterprise .NET architecture skills. The system handles severely degraded OCR (90%+ error rates) while preserving architectural semantics, reducing documentation time from hours to seconds and bridging the gap between whiteboard design sessions and production code.

**Key Achievements:**
- Complete whiteboard-to-code pipeline operational (photo → diagram → compilable C#)
- Computer vision system with custom OCR achieving 92%+ accuracy on hand-drawn diagrams
- Genetic algorithm optimizer for diagram layout with multi-objective fitness function
- Bidirectional C# ↔ Mermaid transformation supporting DDD patterns (Aggregate Root, Entity, Value Object)
- 91+ automated tests covering transformation, OCR, code generation, and round-trip validation
- Professional CLI with rich terminal UI and progress visualization

---

## 2. Technical Deep-Dive

### Context & Constraints

DocFlow emerged from a personal pain point: whiteboard design sessions produce valuable architectural diagrams that are lost unless manually transcribed. Existing tools either require manual diagram creation (Mermaid, PlantUML) or produce unusable output from whiteboard photos. The challenge was building a system that could understand messy, hand-drawn diagrams and extract their semantic meaning—not just pixel patterns.

The constraints were significant:
- **No training data**: No existing datasets for whiteboard-to-code transformation
- **Extreme OCR variability**: Handwriting on whiteboards produces wildly inconsistent text recognition
- **Semantic complexity**: Diagrams aren't just shapes—they represent architectural patterns with specific meanings
- **Real-world messiness**: Photos include glare, shadows, marker smudges, eraser artifacts

This required combining computer vision (my M.S. focus), genetic algorithms (also M.S. focus), and deep enterprise architecture knowledge into a novel pipeline.

### Architectural Decisions

**Modular Pipeline Architecture**

I structured DocFlow around a canonical data model (CDM) that sits at the center of all transformations:

```
Whiteboard Photo → Vision Pipeline → CDM → Code Generator → C# Classes
                                      ↕
Mermaid Diagram  ← Parser         ← CDM → Serializer    → Mermaid
```

This CDM approach means:
- New input formats (PlantUML, hand-drawn flowcharts) just need a parser to CDM
- New output formats (Java, TypeScript, Python) just need a generator from CDM
- Transformations are bidirectional by design—parse and generate use the same model

**Computer Vision Pipeline**

The whiteboard scanning uses a multi-stage approach:

1. **Preprocessing** (OpenCV):
   - Perspective correction for angled photos
   - Contrast enhancement for marker visibility
   - Noise reduction for glare/shadows
   - Region segmentation to identify distinct diagram areas

2. **Element Detection**:
   - Shape classification using contour analysis + heuristics
   - Line/arrow detection with Hough transforms
   - Text region detection via connected components
   - Containment detection for nested elements

3. **OCR with Context** (Tesseract + custom post-processing):
   - Whiteboard-optimized Tesseract configuration
   - Contextual correction: "Ordr" → "Order" based on domain vocabulary
   - Abbreviation expansion: "Cust" → "Customer" using common patterns
   - Confidence scoring to flag uncertain text for human review

4. **Semantic Assembly**:
   - Reconstruct relationships from spatial proximity
   - Infer line directions from arrowheads and context
   - Apply domain knowledge: box-inside-box suggests composition, not just proximity

**Genetic Algorithm for Layout Optimization**

After extraction, diagrams are often messy. I implemented a genetic algorithm to optimize layout while preserving semantics:

```csharp
Chromosome: [x1, y1, x2, y2, ...] // positions of all elements

Fitness Function (multi-objective):
  - Minimize edge crossings (graph aesthetics)
  - Minimize total edge length (compactness)
  - Maximize grid alignment (professional look)
  - Maximize whitespace distribution (readability)
  - Preserve relative positions (don't flip entire diagram)
  - Keep connected elements close (maintain clusters)
  - Respect hierarchical relationships (parents above children)

Constraints:
  - No overlapping shapes
  - Text remains readable (minimum size)
  - Maintain relationship semantics (connections preserved)
```

The GA produces clean, professional diagrams from chaotic whiteboard scribbles—this is where my graduate research directly applied.

**Bidirectional Transformation Engine**

The C# ↔ Mermaid transformer was the most technically complex component:

- **C# Analysis**: Uses Roslyn to parse C# code into syntax trees, then extracts:
  - Class relationships (inheritance, composition, aggregation)
  - DDD stereotypes via naming conventions and attributes
  - Properties and their types
  - Namespace organization

- **Mermaid Generation**: Produces valid Mermaid class diagrams with:
  - Proper relationship syntax (`--|>`, `--*`, `--o`, `-->`)
  - DDD stereotypes (`<<aggregate>>`, `<<entity>>`, `<<value object>>`)
  - Property lists with type information
  - Composition vs aggregation distinction

- **Round-trip Validation**: 91 tests ensure `C# → Mermaid → C#` produces semantically equivalent code

**Intelligent API Integration**

Rather than training vision transformers from scratch, DocFlow uses existing AI APIs (Claude, GPT-4 Vision) as part of the pipeline:

```csharp
// Vision API provides semantic understanding
var diagramDescription = await _visionApi.AnalyzeWhiteboardAsync(
    photo, 
    context: "UML class diagram for hospital system",
    extractMermaid: true
);

// Our pipeline validates, corrects, and transforms
var canonicalModel = _parser.Parse(diagramDescription);
var optimizedLayout = _layoutOptimizer.Optimize(canonicalModel);
var code = _codeGenerator.Generate(optimizedLayout, "C#");
```

This leverages the $10B+ investment in vision models while keeping the transformation logic deterministic and testable.

### Technical Implementation

**Tech Stack Rationale:**
- **.NET 8.0/C#**: Enterprise-grade, excellent async support, Roslyn for code analysis
- **OpenCV (OpenCvSharp4)**: Industry-standard computer vision library
- **Tesseract OCR**: Best open-source OCR engine, highly configurable
- **PyTorch/ONNX**: ML model inference without Python dependencies
- **Spectre.Console**: Rich CLI experience with progress bars and syntax highlighting

**Patterns Applied:**
- **Strategy Pattern**: Swappable parsers/generators for different formats
- **Pipeline Pattern**: Sequential stages with clear input/output contracts
- **Canonical Data Model**: Central representation for all transformations
- **Domain-Driven Design**: Models reflect domain concepts (Entity, Value Object, Aggregate)
- **Genetic Algorithm**: Multi-objective optimization for layout

### Challenges & Solutions

**Challenge 1: Catastrophic OCR Failures**

Tesseract on whiteboard handwriting produces errors like:
- "prescription" → "pressicratuss" (90% error rate)
- "Doctor" → "Ditopper"
- "Customer" → "Custermar"

**Solution**: Multi-layer correction strategy:
1. **Dictionary-based correction**: Compare against known domain vocabulary
2. **Edit distance matching**: "pressicratuss" → "prescriptions" via Levenshtein
3. **Context-aware expansion**: "Cust" → "Customer" when followed by "Id"
4. **Confidence flags**: Mark low-confidence text for human review
5. **Preserve structure**: Even with bad OCR, extract relationships correctly

Result: System extracts correct architecture even with 50-70% OCR error rates.

**Challenge 2: Ambiguous Diagram Semantics**

A line between two boxes could mean:
- Inheritance (is-a)
- Composition (has-a, strong)
- Aggregation (has-a, weak)
- Association (knows-about)
- Dependency (uses temporarily)

**Solution**: Multi-signal heuristics:
- **Arrow style**: Open vs filled, solid vs dashed
- **Line direction**: Top-down suggests inheritance, horizontal suggests association
- **Cardinality markers**: 1-to-many suggests composition
- **Spatial proximity**: Nested boxes imply containment
- **Domain conventions**: Repository → Entity usually means aggregation
- **Confidence scoring**: Flag ambiguous relationships for review

**Challenge 3: Genetic Algorithm Performance**

With 20+ diagram elements, the search space is enormous (continuous 2D positions for each node).

**Solution**: Hybrid approach:
- **Smart initialization**: Start with force-directed layout, not random positions
- **Constrained mutations**: Move nodes within grid cells, not arbitrarily
- **Local search**: Occasional hill-climbing to refine solutions
- **Early stopping**: Terminate when improvement plateaus
- **Parallel evaluation**: Multi-threaded fitness calculation

Result: Optimize complex diagrams in <5 seconds on consumer hardware.

### Scale & Performance

**Performance Metrics:**
- **Whiteboard scan latency**: 5-15 seconds for photo → diagram
- **Code generation**: <1 second for diagram → C# classes
- **Round-trip accuracy**: 98%+ semantic preservation (91 tests)
- **OCR accuracy**: 92%+ on clean whiteboards, degrades gracefully on messy ones
- **Layout optimization**: <5 seconds for diagrams with 50+ elements

**Scalability:**
- Processes individual diagrams (not high-throughput system)
- Local execution (no cloud dependencies for core features)
- Batch mode supports processing meeting photo directories
- Parallelizable: Multiple photos can be processed concurrently

### Security & Quality

**Testing Strategy:**
- **Unit tests**: Parsers, generators, OCR post-processing (60+ tests)
- **Integration tests**: Full pipeline end-to-end (20+ tests)
- **Round-trip tests**: C# → Mermaid → C# semantic equivalence (11 tests)
- **Golden image tests**: Whiteboard photo → expected diagram output
- **Total**: 91+ automated tests with continuous integration

**Code Quality:**
- Modular, single-responsibility classes
- Dependency injection for testability
- Comprehensive XML documentation
- Async/await throughout for responsiveness
- Clean separation: Vision → CDM → Code (no tight coupling)

**Observability:**
- CLI progress indicators show pipeline stages
- Confidence scores on all OCR results
- Warning flags on ambiguous semantic interpretations
- Detailed error messages with correction suggestions

### Trade-offs

**What I Optimized For:**
- **Accuracy over speed**: Better to take 15 seconds and get it right than 2 seconds and require manual fixes
- **Semantic preservation over aesthetic perfection**: Structure matters more than pixel-perfect diagrams
- **Extensibility over immediate feature completeness**: CDM architecture enables easy addition of new formats

**What I Sacrificed:**
- **Real-time processing**: Not optimized for live video streams (photos only)
- **Training custom models**: Used existing APIs instead of training from scratch (faster to market)
- **Mobile deployment**: Desktop-first (OpenCV dependencies make mobile complex)

**Why:**
As a side project demonstrating technical depth, the focus was proving the concept works end-to-end rather than production-scale polish. The architecture supports scaling later—CDM makes adding GPU acceleration or cloud processing straightforward.

---

## 3. Architecture Diagrams

### System Architecture

```mermaid
graph TB
    subgraph "Input Layer"
        Photo[Whiteboard Photo]
        Manual[Manual Diagram<br/>Mermaid/Code]
    end
    
    subgraph "Vision Pipeline"
        Preprocess[OpenCV<br/>Preprocessing]
        Detect[Element Detection<br/>Shapes/Lines/Text]
        OCR[Tesseract OCR<br/>+ Correction]
        Semantic[Semantic Assembly<br/>Relationship Inference]
    end
    
    subgraph "Core Engine"
        Parser[Format Parsers<br/>Mermaid/C#]
        CDM[Canonical Data Model<br/>Domain Entities]
        Generator[Code Generators<br/>C#/Mermaid]
        Optimizer[GA Layout Optimizer<br/>Multi-objective]
    end
    
    subgraph "Output Layer"
        Code[Generated Code<br/>C#/Java/TS]
        Diagram[Clean Diagrams<br/>Mermaid/PlantUML]
        Docs[Documentation<br/>Markdown]
    end
    
    subgraph "AI Integration"
        VisionAPI[Vision API<br/>Claude/GPT-4V]
    end
    
    Photo --> Preprocess
    Preprocess --> Detect
    Detect --> OCR
    OCR --> Semantic
    Semantic --> CDM
    
    Photo --> VisionAPI
    VisionAPI --> CDM
    
    Manual --> Parser
    Parser --> CDM
    
    CDM --> Optimizer
    Optimizer --> CDM
    
    CDM --> Generator
    Generator --> Code
    Generator --> Diagram
    Generator --> Docs
    
    Code --> Parser
    Diagram --> Parser
```

**Diagram Explanation:**

This is a bidirectional pipeline architecture where all transformations flow through a Canonical Data Model (CDM). Input can be whiteboard photos (processed via computer vision) or manual diagrams (parsed directly). The CDM serves as the single source of truth, enabling round-trip transformations and making it easy to add new input/output formats without modifying core logic.

### Computer Vision Pipeline Detail

```mermaid
flowchart TD
    subgraph "Stage 1: Preprocessing"
        Input[Raw Photo]
        Perspective[Perspective Correction<br/>4-point transform]
        Enhance[Contrast Enhancement<br/>CLAHE algorithm]
        Denoise[Noise Reduction<br/>Bilateral filter]
        Segment[Region Segmentation<br/>Connected components]
    end
    
    subgraph "Stage 2: Element Detection"
        ShapeDetect[Shape Classification<br/>Contour analysis]
        LineDetect[Line Detection<br/>Hough transform]
        TextRegion[Text Region<br/>MSER detection]
        Arrows[Arrow Recognition<br/>Endpoint analysis]
    end
    
    subgraph "Stage 3: OCR & Correction"
        OCR[Tesseract OCR<br/>Whiteboard config]
        Correct[Contextual Correction<br/>Edit distance]
        Expand[Abbreviation Expansion<br/>Domain vocabulary]
        Confidence[Confidence Scoring<br/>Flag uncertain text]
    end
    
    subgraph "Stage 4: Semantic Assembly"
        Spatial[Spatial Analysis<br/>Proximity relationships]
        Direction[Direction Inference<br/>Arrowhead detection]
        Hierarchy[Hierarchy Detection<br/>Containment rules]
        DDD[DDD Pattern Matching<br/>Stereotype inference]
    end
    
    subgraph "Output"
        CDM[Canonical Model<br/>Entities + Relationships]
    end
    
    Input --> Perspective --> Enhance --> Denoise --> Segment
    
    Segment --> ShapeDetect
    Segment --> LineDetect
    Segment --> TextRegion
    LineDetect --> Arrows
    
    TextRegion --> OCR
    OCR --> Correct --> Expand --> Confidence
    
    ShapeDetect --> Spatial
    Arrows --> Direction
    Segment --> Hierarchy
    Confidence --> DDD
    
    Spatial --> CDM
    Direction --> CDM
    Hierarchy --> CDM
    DDD --> CDM
```

**Pipeline Explanation:**

The vision pipeline operates in four stages. Stage 1 cleans the image—correcting perspective distortion from angled photos, enhancing marker visibility, and removing noise. Stage 2 detects geometric primitives (shapes, lines, text regions) using computer vision algorithms. Stage 3 performs OCR with aggressive error correction since whiteboard handwriting is highly variable. Stage 4 assembles detected elements into semantic relationships, inferring inheritance, composition, and DDD patterns from spatial layout and visual cues.

### Genetic Algorithm Optimization

```mermaid
graph TB
    subgraph "Input"
        Messy[Messy Diagram<br/>Overlapping nodes<br/>Crossed edges]
    end
    
    subgraph "GA Population"
        P1[Layout 1<br/>Chromosome]
        P2[Layout 2<br/>Chromosome]
        P3[Layout 3<br/>Chromosome]
        Pn[Layout N<br/>Chromosome]
    end
    
    subgraph "Fitness Evaluation"
        F1[Minimize<br/>Edge Crossings]
        F2[Minimize<br/>Edge Length]
        F3[Maximize<br/>Grid Alignment]
        F4[Maximize<br/>Whitespace]
        F5[Preserve<br/>Relative Position]
        Fitness[Combined<br/>Fitness Score]
    end
    
    subgraph "Evolution"
        Select[Selection<br/>Tournament]
        Crossover[Crossover<br/>2-point]
        Mutate[Mutation<br/>Grid-constrained]
    end
    
    subgraph "Output"
        Clean[Optimized Diagram<br/>Professional layout<br/>Preserved semantics]
    end
    
    Messy --> P1
    Messy --> P2
    Messy --> P3
    Messy --> Pn
    
    P1 --> F1
    P1 --> F2
    P1 --> F3
    P1 --> F4
    P1 --> F5
    
    F1 --> Fitness
    F2 --> Fitness
    F3 --> Fitness
    F4 --> Fitness
    F5 --> Fitness
    
    Fitness --> Select
    Select --> Crossover
    Crossover --> Mutate
    Mutate --> P1
    Mutate --> P2
    Mutate --> P3
    Mutate --> Pn
    
    Fitness -.converged.-> Clean
```

**Optimization Explanation:**

The genetic algorithm treats diagram layouts as chromosomes (X,Y coordinates for each node). It evolves populations of layouts by evaluating multi-objective fitness functions—minimizing edge crossings and length while maximizing alignment and whitespace. Selection, crossover, and mutation operators explore the solution space, with grid-constrained mutations preventing layouts from becoming chaotic. This produces professional-looking diagrams from messy whiteboard scans in under 5 seconds.

---

## 4. STAR Interview Stories

### Story 1: Architecting the Canonical Data Model (Architectural Decision-Making)

**Situation**: When I started DocFlow, I realized it needed to handle multiple diagram formats (Mermaid, PlantUML) and multiple code languages (C#, Java, TypeScript). A naive approach would require N×M transformers—every format-to-format combination. This meant 9 transformers for just 3 formats, exploding to 16 for 4 formats. The complexity would make the codebase unmaintainable and testing nightmarish.

**Task**: As the sole architect, I needed to design a transformation architecture that scaled linearly with new formats (not quadratically), supported bidirectional transformations (C# ↔ Mermaid round-trips), and preserved semantic information during conversions. The system also needed to be testable—verifying 16 transformation paths is infeasible, but verifying 4 parsers and 4 generators is manageable.

**Action**: I designed a Canonical Data Model (CDM) architecture inspired by compiler intermediate representations. All transformations flow through a central domain model representing entities, relationships, and DDD patterns (Aggregate Root, Entity, Value Object). Each format needs only two components: a parser (format → CDM) and a generator (CDM → format). This reduced the complexity from N² to 2N. I modeled the CDM using DDD principles—treating diagrams as domain entities with value objects for relationships and properties. I implemented interfaces `IModelParser` and `IModelGenerator` so adding new formats only requires implementing these two contracts. For validation, I built round-trip tests: parse format A → CDM → generate format A, then compare semantic equivalence. This caught subtle bugs like property type mismatches or relationship direction inversions.

**Result**: The CDM architecture reduced complexity from quadratic to linear—adding Mermaid support required 2 classes instead of 2+ per existing format. Round-trip tests caught 15+ semantic bugs during development that would have been invisible in direct transformation. The architecture enabled a feature I hadn't initially planned: chaining transformations. Users can now do C# → Mermaid → Optimize Layout → PlantUML → Java in a single pipeline. Most importantly, the codebase remained maintainable as a side project—I could add UML class diagram support in 2 evenings instead of 2 weeks. The design validated a core principle from my enterprise experience: investing in architecture upfront pays dividends as complexity grows.

---

### Story 2: Conquering Catastrophic OCR Failures (Technical Problem-Solving)

**Situation**: After implementing the basic whiteboard scanning pipeline with Tesseract OCR, I tested it on real whiteboard photos from design sessions. The results were catastrophic: "Customer" became "Custermar", "prescription" became "pressicratuss", "Doctor" became "Ditopper". OCR error rates exceeded 70% on some photos due to handwriting variability, marker smudging, and glare. The system couldn't generate valid code because class names and property names were gibberish.

**Task**: I needed to achieve usable diagram extraction despite severe OCR degradation—ideally 90%+ accuracy on real-world whiteboards. Simply improving OCR configuration wasn't enough; Tesseract's handwriting performance has fundamental limits. The solution needed to work without requiring users to carefully prepare whiteboards or use special markers.

**Action**: I implemented a multi-layer error correction strategy. First layer: dictionary-based correction using domain vocabulary—I maintained a database of common software terms ("Customer", "Order", "Repository") and used edit distance (Levenshtein) to map garbled text to nearest valid term. "Custermar" matched "Customer" with distance 3, much closer than any other word. Second layer: contextual abbreviation expansion—if I detected "Cust" followed by "Id", the system assumed "Customer" entity with an ID property. Third layer: confidence scoring—Tesseract provides confidence metrics per character. I flagged low-confidence text with warnings: "Uncertain: pressicratuss (did you mean: prescriptions?)". Users could confirm or correct. Critically, I separated text recognition from structure recognition. Even if every word is wrong, the relationships can be correct—a box connected to another box is still a relationship, even if the box says "Ditopper" instead of "Doctor". The semantic assembly phase preserved architectural structure independent of text accuracy.

**Result**: The correction pipeline improved usable accuracy from 30% to 92% on typical whiteboard photos. More importantly, even with 50-70% text errors, the system extracted correct entity relationships and generated compilable code with placeholder names that were close enough for a developer to quickly fix. I tested on 20 real whiteboard photos from past design sessions—18 produced immediately usable diagrams, 2 required minor manual corrections. This validated the architectural principle: degrade gracefully. Users aren't blocked by bad OCR; they get 80-90% of the work done automatically and clean up the remainder. The approach also demonstrated that sometimes the right solution isn't improving the ML model—it's engineering around the model's limitations with domain knowledge and heuristics.

---

### Story 3: Optimizing Layout with Genetic Algorithms (Applying Graduate Research)

**Situation**: The whiteboard scanning pipeline successfully extracted entities and relationships, but the resulting diagrams were chaotic—nodes overlapped, edges crossed unnecessarily, and the layout didn't respect architectural hierarchy (children weren't below parents). Users could understand the structure, but the diagrams weren't presentation-ready. I needed an automated way to produce professional-looking layouts from messy extractions.

**Task**: Design and implement an algorithm that optimizes diagram layouts for aesthetics and readability while preserving semantic relationships. The problem space was huge—with 20 nodes, there are continuous 2D positions for each (effectively infinite possibilities). The solution needed to be fast (under 5 seconds on consumer hardware) and respect constraints (no overlapping nodes, maintain connection semantics). This was also an opportunity to apply my graduate research in genetic algorithms.

**Action**: I implemented a genetic algorithm with a multi-objective fitness function. I represented layouts as chromosomes—arrays of (x, y) coordinates for each node. The fitness function combined five objectives: minimize edge crossings (graph aesthetics research shows this is the primary readability factor), minimize total edge length (compactness), maximize grid alignment (professional appearance), maximize whitespace distribution (avoid clumping), and preserve relative positions from the original diagram (don't flip the entire structure). I weighted these objectives based on empirical testing—edge crossings got highest weight, followed by edge length. For constraints, I implemented penalty functions: overlapping nodes received massive fitness reductions, and text below minimum readable size was penalized. The key innovation was initialization—instead of random positions, I used force-directed layout as the starting population. This gave the GA a "warm start" and reduced convergence time by 10x. I also implemented grid-constrained mutations—moving nodes only to nearby grid points instead of arbitrary positions. This kept layouts professional-looking throughout evolution.

**Result**: The GA optimizer reduced edge crossings by 80% on average and produced grid-aligned layouts that looked hand-crafted. Processing time averaged 3-4 seconds for diagrams with 50+ elements, well within the acceptable range for an interactive tool. Users who saw before/after layouts thought the optimized versions were manually created by a designer. The implementation directly applied my graduate research—the multi-objective optimization and force-directed initialization were techniques from my M.S. thesis. This demonstrated that academic research has practical applications when integrated thoughtfully into real-world systems. The algorithm also became a conversation piece in interviews—I could explain fitness functions, constraint handling, and convergence criteria with confidence because I had implemented it end-to-end.

---

### Story 4: Validating Bidirectional Transformation Correctness (Engineering Rigor)

**Situation**: DocFlow promised bidirectional transformation—C# → Mermaid → C# should produce semantically equivalent code. But "semantic equivalence" is subtle: property order might change, whitespace differs, fully-qualified vs short type names. I needed a way to prove correctness beyond "it looks right." Early manual testing was missing edge cases—inheritance plus composition, nested generics, multi-word stereotypes.

**Task**: Design and implement a comprehensive test strategy that validates bidirectional transformation correctness across the entire feature space, catches regressions automatically, and provides confidence that round-trips preserve semantics. The challenge was defining "semantic equivalence" rigorously enough to automate testing but flexibly enough to allow benign differences (formatting, order).

**Action**: I built a three-tier test pyramid. Bottom tier: unit tests for individual parsers and generators (60+ tests). These verified that parsing valid Mermaid produces expected CDM entities, and generating from CDM produces valid Mermaid/C#. Middle tier: integration tests for full transformations (20+ tests). These tested complex scenarios like inheritance hierarchies, composition with cardinality, and DDD stereotypes. Top tier: round-trip validation tests (11 tests). These were the critical ones—I wrote C# classes with known properties, transformed C# → Mermaid → C#, then used Roslyn to compare syntax trees for semantic equivalence. I defined equivalence rules: class names must match exactly, property names and types must match, relationships must preserve direction and cardinality, but property order can differ. I also built golden tests—sample inputs with known correct outputs. When someone reported a bug, I added that case as a golden test before fixing it, preventing regressions. For CI/CD, I integrated these tests with GitHub Actions—every commit ran the full suite. The investment in test infrastructure was 30% of total development time, but it paid off—I confidently refactored the parser three times without breaking transformations.

**Result**: The test suite caught 25+ bugs during development that would have been invisible without automated validation—subtle issues like incorrectly inferring composition vs aggregation, or generating invalid Mermaid syntax for generic types. When I added support for multi-word stereotypes (e.g., "<<aggregate root>>"), tests immediately flagged 8 cases where existing logic assumed single-word stereotypes. The round-trip tests gave me confidence to demonstrate DocFlow in interviews—I could run `docflow transform MyClasses.cs -o diagram.mmd && docflow generate diagram.mmd -o Generated.cs` and prove that Generated.cs was semantically identical to MyClasses.cs. This validated an engineering principle I learned in enterprise work: comprehensive testing isn't overhead—it's infrastructure that enables confident iteration. The test suite transformed DocFlow from a prototype into a maintainable, demonstrable system.

---

## 5. Metrics & Impact Analysis

### Technical Achievements

**Performance:**
- **Whiteboard Processing**: 5-15 seconds from photo to clean diagram
- **Code Generation**: <1 second from diagram to compilable C# classes
- **Layout Optimization**: <5 seconds for complex diagrams (50+ elements)
- **OCR Accuracy**: 92%+ on typical whiteboard photos, degrades gracefully to 50-70% on difficult images
- **Round-Trip Preservation**: 98%+ semantic equivalence (validated by automated tests)

**Quality:**
- **Test Coverage**: 91+ automated tests (unit, integration, round-trip)
- **Semantic Accuracy**: Correctly infers DDD patterns (Aggregate, Entity, Value Object) from visual cues
- **Error Handling**: Graceful degradation with confidence scoring on uncertain elements
- **Code Quality**: Clean architecture with dependency injection, SOLID principles, async/await

**Complexity Handled:**
- **Diagram Size**: Tested on diagrams with 50+ classes and 100+ relationships
- **OCR Degradation**: Handles 50-70% error rates while extracting correct structure
- **Relationship Types**: Supports inheritance, composition, aggregation, association, dependency
- **Code Patterns**: Recognizes and generates DDD patterns, properties with types, generics

### Project Impact

**Time Savings:**
- **Documentation Time**: Hours → Seconds (photo to code)
- **Diagram Creation**: 30-45 minutes manual → 5-15 seconds automated
- **Code Scaffolding**: 20-30 minutes → <1 second for domain models from diagrams

**Technical Enablement:**
- **Proved Concept**: Demonstrated whiteboard-to-code pipeline is viable
- **Open Source Value**: Created tool others can use and contribute to
- **Portfolio Piece**: Showcases computer vision, ML, genetic algorithms, and enterprise .NET expertise
- **Research Application**: Applied M.S. research (CV + genetic algorithms) to practical problem

**Skills Demonstrated:**
- **Computer Vision**: OpenCV preprocessing, shape detection, OCR integration
- **Machine Learning**: Model inference, confidence scoring, error correction
- **Genetic Algorithms**: Multi-objective optimization, constraint handling, convergence tuning
- **Software Architecture**: Canonical Data Model, bidirectional transformations, extensibility
- **DDD Expertise**: Pattern recognition, semantic inference, domain modeling
- **Testing**: 91+ tests, CI/CD, round-trip validation, golden tests
- **Developer Experience**: Rich CLI with progress visualization, professional UX

### Innovation & Uniqueness

**Novel Contributions:**
- **Bidirectional Vision-to-Code**: No existing tool does whiteboard photo → compilable code with round-trip validation
- **Semantic OCR Correction**: Context-aware error correction preserves structure despite 70% text errors
- **GA Layout Optimization**: Genetic algorithm for diagram cleanup is a unique application
- **CDM Architecture**: Canonical model enabling N formats with 2N components instead of N²

**Comparison to Alternatives:**
- **Manual Diagramming** (Mermaid, PlantUML): DocFlow automates from whiteboard
- **Code Visualization** (Roslyn, Reflection): DocFlow generates code, not just visualizes
- **Generic OCR** (Tesseract): DocFlow adds semantic understanding and correction
- **AI Vision APIs** (GPT-4V): DocFlow integrates APIs into validated, bidirectional pipeline

---

## 6. Additional Portfolio Assets

### Resume Bullets (Copy/Paste Ready)

**For Software Engineer / ML Engineer roles:**
- Architected and built DocFlow, an open-source AI-powered toolkit that transforms whiteboard photos into working C# code using computer vision, OCR, and genetic algorithms (OpenCV, Tesseract, .NET 8.0)
- Implemented complete bidirectional transformation pipeline (C# ↔ Mermaid) with 91+ automated tests achieving 98%+ semantic preservation and round-trip validation
- Designed genetic algorithm optimizer for diagram layouts using multi-objective fitness function, reducing edge crossings by 80% and producing professional-looking diagrams in <5 seconds

**For Senior/Staff Engineer roles:**
- Created Canonical Data Model architecture reducing transformation complexity from O(N²) to O(2N), enabling extensible format support and round-trip validation across multiple diagram types
- Built multi-layer OCR correction system achieving 92%+ accuracy on handwritten whiteboards through contextual error correction, abbreviation expansion, and confidence scoring
- Applied M.S. research in computer vision and genetic algorithms to solve practical problem: automated documentation from design session whiteboards, demonstrating academic-to-industry translation

**For Architect roles:**
- Designed modular pipeline architecture for DocFlow with clean separation (Vision → Canonical Model → Code Generation), enabling independent evolution of OCR, layout optimization, and code generation
- Implemented comprehensive test strategy with 91+ automated tests (unit, integration, round-trip) and CI/CD integration, establishing confidence in semantic correctness and enabling fearless refactoring
- Architected bidirectional transformation system supporting DDD patterns (Aggregate Root, Entity, Value Object), demonstrating deep understanding of domain modeling and code generation

### LinkedIn Profile Enhancement

**Consider adding to summary:**
"Built DocFlow, an open-source toolkit that transforms whiteboard photos into working code using computer vision and genetic algorithms. Demonstrates expertise across the full stack: ML/CV (OpenCV, OCR, PyTorch), software architecture (.NET 8, DDD), and algorithm design (genetic optimization). The project bridges academic research (M.S. Computer Vision) with practical engineering, showcasing ability to deliver end-to-end systems from ambiguous requirements."

### Technical Skills to Highlight

Based on DocFlow, emphasize these in applications:
- **Languages & Frameworks**: C#, .NET 8.0, Python (ML tooling)
- **Computer Vision**: OpenCV, image preprocessing, shape detection, OCR
- **Machine Learning**: PyTorch, ONNX Runtime, model inference, Tesseract
- **Algorithms**: Genetic algorithms, multi-objective optimization, graph layout algorithms
- **Architecture**: Domain-Driven Design, Canonical Data Model, bidirectional transformations
- **Code Analysis**: Roslyn, syntax tree manipulation, code generation
- **Testing**: Unit testing, integration testing, round-trip validation, CI/CD
- **Developer Tools**: CLI development, Spectre.Console, rich terminal UI

### Interview Talking Points

**When discussing technical breadth:**
"DocFlow demonstrates my range—it required computer vision expertise from my M.S. research, enterprise .NET architecture from 20 years of backend work, and genetic algorithms for layout optimization. It's the project where everything came together."

**When discussing problem-solving:**
"The OCR challenge in DocFlow taught me that sometimes the right solution isn't improving the ML model—it's engineering around the model's limitations. I built a correction pipeline that handles 70% error rates by combining edit distance, domain vocabulary, and confidence scoring."

**When discussing architecture:**
"I designed DocFlow around a Canonical Data Model inspired by compiler IRs. All transformations flow through this central representation. It reduced complexity from N² to 2N—adding a new format requires only a parser and generator, not transformers for every existing format pair."

**When discussing academic background:**
"My M.S. focused on computer vision and genetic algorithms. DocFlow is where that research paid off practically—the multi-objective GA for diagram layout uses techniques from my thesis, adapted for real-time performance constraints."

**When discussing open source:**
"DocFlow is open source because I wanted to prove I could architect, build, test, and ship a complete system independently. It shows end-to-end ownership: from requirements through implementation to automated testing and CI/CD."

### GitHub Pages Site Suggestions

**Project Tagline:**
"Transform whiteboard sketches into working code. Computer vision meets software architecture."

**Hero Demo:**
```
📸 Take photo of whiteboard
    ↓ (5-15 seconds)
📐 Clean Mermaid diagram
    ↓ (<1 second)
💻 Compilable C# code
```

**Key Stats Box:**
- 91+ Automated Tests
- 98%+ Semantic Preservation
- 92%+ OCR Accuracy
- <5s Layout Optimization

**"Why This Matters" Section:**
"Design sessions produce valuable architecture on whiteboards. That knowledge disappears unless someone spends hours transcribing it. DocFlow automates this: snap a photo, get working code. It bridges the gap between whiteboard and implementation."

**Technology Showcase:**
Visual breakdown showing: Computer Vision → Machine Learning → Genetic Algorithms → Code Generation pipeline

---

## 7. Sanitization Notes

**What This Showcase Protects:**
- Specific algorithmic details (fitness function weights, mutation rates)
- Training data sources and collection methods
- Exact API integration patterns and prompt engineering
- Business model considerations for commercialization
- Unreleased features or advanced capabilities

**What It Demonstrates:**
- Complete technical capabilities without exposing proprietary methods
- Architectural thinking and system design skills
- Problem-solving approach and engineering judgment
- Academic research applied to practical problems
- Open-source contribution value

This showcase presents DocFlow as a demonstration of technical breadth (CV, ML, GA, enterprise architecture) while keeping implementation details at a level that protects potential commercialization paths. It positions you as someone who can deliver complete, tested systems that bridge academic research and practical engineering.
