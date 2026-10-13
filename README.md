# Introduction
Description of the project

# Pseudocode
```
#Project04 Pseudocode

"""De Bruijn Graph Genome Assembly Module.

This module provides classes and functions for constructing De Bruijn graphs
from sequencing reads and performing genome assembly using Eulerian path
traversal.
"""
from collections import defaultdict
import random


class DeBruijnGraph:
    """Main class for De Bruijn graphs and genome assembly.

    This class builds De Bruijn graphs from sequencing reads and performs
    genome assembly by finding Eulerian paths through connected components
    of the graph.

    Attributes:
        graph (defaultdict): Adjacency list representation of graph edges.
            Keys are (k-1)-mers, values are lists of adjacent (k-1)-mers.
        k (int): The k-mer size used for graph construction.

    Example:
        >>> reads = ["ATGGCGTACG", "GCGTACGTTA", "ACGTTACCAT"]
        >>> dbg = DeBruijnGraph(reads, k=6)
        >>> contigs = dbg.assemble_contigs(seed=42)
        >>> len(contigs) > 0
        True
    """

    def __init__(self, reads, k):
        """Initialize De Bruijn graph from sequencing reads.

        Args:
            reads (list): List of DNA sequence strings.
            k (int): K-mer size for graph construction.

        Example:
            >>> reads = ["ATGGCG", "GCGTGC", "TGCAAC"]
            >>> dbg = DeBruijnGraph(reads, k=4)
            >>> len(dbg.graph) > 0
            True
        """
        self.graph = defaultdict(list)
        self.k = k
        self.build_graph_from_reads(reads, k)

    def add_edge(self, left, right):
        """Add a directed edge to the graph.

        Args:
            left (str): Source (k-1)-mer node.
            right (str): Destination (k-1)-mer node.

        Example:
            >>> dbg = DeBruijnGraph([], k=4)
            >>> dbg.add_edge("ATG", "TGG")
            >>> "TGG" in dbg.graph["ATG"]
            True
        """

        #add right to the end of left's list in self.graph
    
    def remove_edge(self, left, right):
        """Remove a directed edge from the graph.

        Args:
            left (str): Source (k-1)-mer node.
            right (str): Destination (k-1)-mer node.

        Example:
            >>> dbg = DeBruijnGraph([], k=4)
            >>> dbg.add_edge("ATG", "TGG")
            >>> dbg.remove_edge("ATG", "TGG")
            >>> len(dbg.graph["ATG"])
            0
        """
        #remove right from left's list in self.graph

    def build_graph_from_reads(self, reads, k):
        """Build De Bruijn graph from multiple sequencing reads.

        Extracts all k-mers from all reads and adds edges between
        consecutive (k-1)-mers within each k-mer.

        Args:
            reads (list): List of DNA sequence strings.
            k (int): K-mer length for graph construction.

        Example:
            >>> reads = ["ATGGC", "TGGCA"]
            >>> dbg = DeBruijnGraph([], k=4)
            >>> dbg.build_graph_from_reads(reads, 4)
            >>> "ATG" in dbg.graph
            True
        """

        #Sanity-check print statement:  print how many reads there are and the value of k
        #FOR each read in reads:
            #FOR each position, from 0 up to (length of read - k):
                #kmer = the k letters starting at this position
                #left = kmer without its last letter
                #right = kmer without its first letter
                #Sanity-check print statement: print each kmer with its left and right node, first read only
                #IF right is not already in left's list in self.graph:
                    #self.add_edge(left, right)
        #Sanity-check print statement: pring number of nodes, number of edges

    def eulerian_walk(self, node, graph, seed=None):
        """Perform recursive Eulerian walk on a graph component.

        This is a recursive function that follows all edges from a node
        to traverse the graph, building a path in reverse order.

        Args:
            node (str): Current node to traverse from.
            graph (defaultdict): Graph or subgraph to traverse.
            seed (int, optional): Seed for random edge selection.

        Returns:
            list: List of (k-1)-mers traversed (in reverse order).

        Example:
            >>> reads = ["ATGGCG"]
            >>> dbg = DeBruijnGraph(reads, k=4)
            >>> graph_copy = defaultdict(list, dbg.graph)
            >>> tour = dbg.eulerian_walk("ATG", graph_copy, seed=42)
            >>> len(tour) > 0
            True
        """
        #IF a seed was given:
            #set the random seed (only in 1st call)
        #tour = an empty list

        #WHILE node's list in graph is not empty:
            #next node = pick one of node's list in graph at random
            #remove next node from node's list in graph (the copy)
            #tour = tour + self.eulerian_walk(next node, graph)

        #add node to end of tour
        #Return tour

    def assemble_contigs(self, seed=None):
        """Assemble all contigs from the De Bruijn graph.

        Finds all connected components and generates an Eulerian path
        for each component, producing multiple assembled contigs.

        Args:
            seed (int, optional): Random seed for reproducible assembly.

        Returns:
            list: List of assembled contig sequences (DNA strings).

        Example:
            >>> reads = ["ATGGCGTACG", "GCGTACGTTA", "ACGTTACCAT"]
            >>> dbg = DeBruijnGraph(reads, k=6)
            >>> contigs = dbg.assemble_contigs(seed=42)
            >>> all(isinstance(c, str) for c in contigs)
            True
        """
        #IF a seed was given:
            #set the random seed (once for all walks)
        #copy = a new empty graph
        #FOR each node in self.graph:
            #copy's list for node = a copy of node's list
        #Sanity-check print statement: print node count in self.graph and in copy (should match)
        
        #arriving = a count for each node, starting at 0
        #FOR each node in self.graph:
            #FOR each neighbor in node's list:
                #add 1 to arriving for neighbor
        
        #start nodes = every node whose list length (leaving) > its arriving count
        #Sanity-check print statement: print how many start nodes were found

        #all nodes = a list of every node in self.graph, made now, before any walking 
        #contigs = an empty list
        #kept = an empty set

        #FOR each node in (start nodes, followed by all nodes):
            #IF node's list in copy is not empty:
                #tour = self.eulerian_walk (node, copy)
                #Sanity-check print statement: print the length of the tour (first 3 walks only)
                
                #reverse the tour
                #pieces = a list holding one piece: [the first node]
                #FOR each node in the tour after the first:
                    #previous = the last node of the current piece
                    #IF node is in previous's list in self.graph: (real edge, the original)
                        #add node to the current piece
                    #ELSE:
                        #start a new piece with node
                
                #FOR each piece:
                    #IF the piece has at least 2 nodes:
                        #sequence = self.tour_to_sequence(piece)
                        #rc = the reverse complement of sequence
                        #IF neighter sequence or rc is in kept:
                            #add sequence to contigs
                            #add sequence to kept
        
        #Sanity check print statement: print number of contigs
        #Sanity check print statement: print edge count in self.graph (should be unchanged, proving original is intact)
        #Return contigs


    def tour_to_sequence(self, tour):
        """Convert a tour of (k-1)-mers into a DNA sequence.

        Args:
            tour (list): List of (k-1)-mer strings in order.

        Returns:
            str: Assembled DNA sequence.

        Example:
            >>> dbg = DeBruijnGraph([], k=4)
            >>> tour = ['ATG', 'TGG', 'GGC', 'GCG']
            >>> dbg.tour_to_sequence(tour)
            'ATGGCG'
        """
        #sequence = the whole first node in tour
        #FOR each node after the first one:
            #add that node's last letter to the end of sequence
        #Return sequence

    def get_assembly_stats(self, contigs):
        """Calculate assembly statistics for assembled contigs.

        Args:
            contigs (list): List of contig sequences.

        Returns:
            dict: Dictionary containing assembly statistics:
                - num_contigs: Total number of contigs
                - total_length: Total assembled sequence length
                - longest_contig: Length of longest contig
                - shortest_contig: Length of shortest contig
                - mean_length: Mean contig length
                - n50: N50 statistic

        Example:
            >>> contigs = ["ATGGCG", "TTTAAA", "CCCCCCCCCC"]
            >>> dbg = DeBruijnGraph([], k=4)
            >>> stats = dbg.get_assembly_stats(contigs)
            >>> stats['num_contigs']
            3
        """
        #lengths = a list of the length of each contig

        #IF there are no contigs:
            #Return all six stats set to 0

        #num_contigs = how many contigs are there
        #total_length = all lengths added together
        #longest_contig = the biggest length
        #shortest_contig = the smallest length
        #mean_length = total_length / num_contigs

        #sort the lengths, longest first
        #running total = 0
        #FOR each length:
            #add it to the running total
            #IF running total >= total_length / 2
                #n50 = this length
                #stop the loop
        
        #Return a dictionary holding the six stats, under these exact names:
            #num_contigs, total_length, longest_contig, shortest_contig, mean_length, n50

    def write_fasta(self, contigs, filename):
        """Write assembled contigs to a FASTA file.

        Args:
            contigs (list): List of contig sequences.
            filename (str): Output FASTA filename.

        Example:
            >>> contigs = ["ATGGCG", "TTTAAA"]
            >>> dbg = DeBruijnGraph([], k=4)
            >>> dbg.write_fasta(contigs, "output.fasta")
        """
        #open the file called filename, for writing
        #FOR each contig, numbered from 1:
            #write ">contig_" + number + " length=" + length of contig, then a line break
            #write the contig, then a line break
        #close the file
        #Sanity-print check statement:  print the filename and how many contigs were written
```

# Results
================================================================================
GENOME DE BRUIJN GRAPH ASSEMBLY
Student Assignment Driver Program
================================================================================

================================================================================
GENOME ASSEMBLY PIPELINE
================================================================================
Start time: 2026-10-13 05:43:35

STEP 1: Loading sequencing reads
--------------------------------------------------------------------------------
Input file: data/sacCer_R64_150SE_30x_wgsim.fq.gz

Reads loaded: 2,414,266
Total bases: 362,139,900 bp
Average read length: 150.0 bp
Time elapsed: 3.91 seconds

Sample reads:
  First: ATCACAAAGGAGACAAAATCGTTGATAAAAAGTGCATCAACATTCCCAGCCAGAAAATGCACATCATAAAGACATGTTAT...
  Last:  ATTTAGCTCGCTTGTTTCTTGATTTTTTAGTCTCAATTTCATATCGTTAATAAAATCCTTGTGAGCTTCTGAGTTTAAAG...

STEP 2: Building De Bruijn graph
--------------------------------------------------------------------------------
K-mer size: 31
Building graph from 2,414,266 reads...

Graph construction complete!
  Nodes (distinct 30-mers): 22,953,466
  Edges (distinct 31-mers):   22,961,448
  Average out-degree: 1.00
Time elapsed: 366.01 seconds

STEP 3: Assembling contigs
--------------------------------------------------------------------------------
Traversing the graph to build contigs...

Assembly complete!
  Contigs generated: 3,844
Time elapsed: 122.53 seconds

STEP 4: Calculating assembly statistics
--------------------------------------------------------------------------------
Assembly statistics:
  Number of contigs:     3,844
  Total assembly length: 11,592,504 bp
  Longest contig:        108,052 bp
  Shortest contig:       31 bp
  Mean contig length:    3,015.7 bp
  N50:                   25,294 bp

Top 10 longest contigs:
   1. 108,052 bp
   2. 104,496 bp
   3. 93,617 bp
   4. 79,109 bp
   5. 78,359 bp
   6. 77,240 bp
   7. 75,690 bp
   8. 75,295 bp
   9. 74,255 bp
  10. 73,614 bp

Genome coverage analysis:
  Reference genome size:         12,071,326 bp
  Estimated sequencing coverage: 30.0x
  Assembly size vs. genome:      96.0%
  (Near 200% usually means reverse-complement duplicate contigs were not removed.)

STEP 5: Writing output files
--------------------------------------------------------------------------------
✓ Contigs written to: genome_assembly.fasta
✓ Statistics written to: genome_assembly_stats.txt

================================================================================
ASSEMBLY COMPLETE
================================================================================
Total time (excluding file output): 492.45 seconds (8.21 minutes)
End time: 2026-10-13 05:51:57

================================================================================
FIVE LONGEST ASSEMBLED CONTIGS
================================================================================

>contig_1 length=108052
CCTTGTTCGTTGGCAATAATTTCAACGGAGGATTCGTAAGTAGCAACACAAGAGTAGGTTGTACCTAAATCGATACCGATAGCACCTTGGAAAACACCTT...

>contig_2 length=104496
AATGGTCACGGCGTCTGGCTACGAACCAGGAGATTCCAGGTTCGAGTCCTGGCGGGGAAGAATATTCTTTTTGTCACTAACACAACCATTCTATAAATTG...

>contig_3 length=93617
ACTTGGCTCTCAAATCAAGTTATAATTGTATCGGAGAACTACCATTCACCAATTTCACACCGTCATTCACAGATGTTATCGACTATATATGGTTTTCTAC...

>contig_4 length=79109
AATAATAATAATAATAATAGTAATAATAACGTCTATATAAGAAGTATCTACACCATTGCTTACGCTTTTATTTTTTCCTTTCGACGTGAAAAGCGATAAT...

>contig_5 length=78359
TGCTGTTGCTGTTGTTGTTGTTGTTGTTGCTGATGCTGCTGCTGCTGTTGTTGTTGCTTTTGTTGCTGCTGTTGTATTTGCACATGATGCCTAAACTGTT...

================================================================================
✓ ASSEMBLY COMPLETE
================================================================================

Results saved to:
  • genome_assembly.fasta - 3,844 assembled contigs
  • genome_assembly_stats.txt - detailed assembly statistics

Key metrics:
  • Total assembly: 11,592,504 bp
  • N50: 25,294 bp
  • Longest contig: 108,052 bp
  • Coverage: 30.0x

# Successes
Description of the team's learning points

# Struggles
Description of the stumbling blocks the team experienced

# Personal Reflections
## Group Leader
Group leader's reflection on the project

## Other member
Other members' reflections on the project

# Generative AI Appendix
As per the syllabus
