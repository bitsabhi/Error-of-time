errorTimeline.forEach(error => {
  if (error.time <= currentFrame && errorTypes[error.type].temporalViolation) {
    breaches.push({
      operation: error.operation,
      violationType: 'causal_ordering',
      severity: errorTypes[error.type].severity,
      timeViolation: error.causalChain?.length - error.actualChain?.length || 1
    });
  }
});
