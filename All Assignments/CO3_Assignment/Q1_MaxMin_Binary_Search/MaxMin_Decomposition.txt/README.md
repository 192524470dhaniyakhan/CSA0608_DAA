             INPUT ARRAY
          [12, 5, 8, 20, 3, 15]
                    |
              Divide into pairs
                    |
          ---------------------
          |                   |
       (12, 5)             (8, 20)
          |                   |
       Min = 5             Min = 8
       Max = 12            Max = 20

          (3, 15)
              |
          Min = 3
          Max = 15

                    |
             Candidate Lists
                    |
       -------------------------
       |                       |
   Min Candidates         Max Candidates
   [5, 8, 3]              [12, 20, 15]
       |                       |
    Minimum                 Maximum
       |                       |
       3                      20

              FINAL OUTPUT
          Minimum = 3
          Maximum = 20
