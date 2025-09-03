\documentclass{article}
\usepackage{hyperref}
\usepackage{geometry}
\geometry{margin=1in}
\begin{document}

\title{Multivariate MR-PRESSO}
\author{Yuankai Zhang}
\date{\today}
\maketitle

\section*{Overview}
\textbf{Multivariate MR-PRESSO} (Mendelian Randomization Pleiotropy RESidual Sum and Outlier) is an R implementation extending the original univariate MR-PRESSO framework to handle multiple outcomes simultaneously. The package allows detection and correction of horizontal pleiotropy in multivariate Mendelian Randomization (MR) analyses using residual-based statistics and Mahalanobis distance.

This repository contains:
\begin{itemize}
    \item Core function \verb|mr_presso_multivariate| for multivariate outlier detection and distortion testing.
    \item Visualization function \verb|plot_mr_presso_multivariate| for diagnostic plots across multiple outcomes.
    \item Example scripts for running MR-PRESSO on simulated or summary-level data.
\end{itemize}

\section*{Installation}
Clone the repository and source the functions directly:
\begin{verbatim}
git clone https://github.com/<your-username>/mr-presso-multivariate.git
cd mr-presso-multivariate
R
source("mr_presso_multivariate.R")
source("plot_mr_presso_multivariate.R")
\end{verbatim}

\section*{Usage}

\subsection*{Core Function}
\verb|mr_presso_multivariate| performs the following steps:
\begin{enumerate}
    \item Standard MR-IVW regression across exposures and outcomes.
    \item Outlier detection via leave-one-out residuals and Mahalanobis distances.
    \item Empirical null distribution generation by simulation.
    \item Distortion test comparing causal estimates with and without outliers.
    \item Outlier-corrected MR analysis.
\end{enumerate}

\subsection*{Arguments}
\begin{itemize}
    \item \verb|BetaOutcome|: character vector of outcome beta column names.
    \item \verb|BetaExposure|: character vector of exposure beta column names.
    \item \verb|SdOutcome|: character vector of outcome standard error column names.
    \item \verb|SdExposure|: character vector of exposure standard error column names.
    \item \verb|data|: data frame with summary statistics.
    \item \verb|OUTLIERtest|: logical, whether to perform outlier test.
    \item \verb|DISTORTIONtest|: logical, whether to perform distortion test.
    \item \verb|SignifThreshold|: numeric, significance threshold for outlier detection.
    \item \verb|NbDistribution|: integer, number of simulations for empirical $p$-values.
    \item \verb|seed|: optional random seed.
\end{itemize}

\subsection*{Return Value}
The function returns a list containing:
\begin{itemize}
    \item \textbf{Main MR results:} raw and outlier-corrected causal estimates.
    \item \textbf{MR-PRESSO results:} global test, outlier test, and distortion test outputs.
\end{itemize}

\section*{Visualization}
The function \verb|plot_mr_presso_multivariate| provides diagnostic plots:
\begin{itemize}
    \item Outlier detection Manhattan-style plot.
    \item Forest plot comparing raw vs. outlier-corrected causal estimates.
    \item Standardized residual diagnostic plots.
    \item Q-Q plot of Mahalanobis distances.
\end{itemize}

\section*{Example}
\begin{verbatim}
results <- mr_presso_multivariate(
  BetaOutcome   = c("beta_Y1", "beta_Y2"),
  BetaExposure  = c("beta_X1", "beta_X2"),
  SdOutcome     = c("se_Y1", "se_Y2"),
  SdExposure    = c("se_X1", "se_X2"),
  data          = summary_data,
  OUTLIERtest   = TRUE,
  DISTORTIONtest= TRUE,
  NbDistribution= 1000,
  seed          = 1234
)

plots <- plot_mr_presso_multivariate(
  mr_results   = results,
  data         = summary_data,
  BetaOutcome  = c("beta_Y1", "beta_Y2"),
  BetaExposure = c("beta_X1", "beta_X2"),
  plot_type    = "all"
)
\end{verbatim}

\section*{Citation}
If you use this code, please cite the original MR-PRESSO paper:

\begin{quote}
Verbanck, M., Chen, C. Y., Neale, B., \& Do, R. (2018). 
Detection of widespread horizontal pleiotropy in causal relationships inferred from Mendelian randomization between complex traits and diseases. 
\textit{Nature Genetics}, 50(5), 693--698.
\end{quote}



\end{document}
