import { useState, useMemo } from "react";
import {
  TextField,
  IconButton,
  Collapse,
  Box,
  Typography,
} from "@mui/material";
import ExpandMoreIcon from "@mui/icons-material/ExpandMore";
import { DataGrid, GridColDef } from "@mui/x-data-grid";
import type { FormAbertura } from "./Abertura";

type Props = {
  dados: FormAbertura[];
};

export default function TabelaAcompanhamento({ dados }: Props) {
  const [showFilters, setShowFilters] = useState(false);
  const [search, setSearch] = useState("");
  const [status, setStatus] = useState("Todos");

  const filteredRows = useMemo(() => {
    return dados
      .map((d, i) => ({ id: i + 1, ...d }))
      .filter((row) => {
        const matchSearch =
          search === "" ||
          Object.values(row)
            .join(" ")
            .toLowerCase()
            .includes(search.toLowerCase());

        // Se não tem status no FormAbertura, isso sempre vira true
        const matchStatus = true;

        return matchSearch && matchStatus;
      });
  }, [dados, search, status]);

  //  COLUNAS SIMPLES BASEADAS EM FORMABERTURA
  const columns: GridColDef[] = [
    { field: "solicitante", headerName: "Solicitante", flex: 1 },
    { field: "areaSolicitante", headerName: "Área", flex: 1 },
    { field: "titulo", headerName: "Título", flex: 1 },
    { field: "motivacao", headerName: "Motivação", flex: 1 },
    { field: "dataHora", headerName: "Data/Hora", flex: 1 },
    { field: "descricao", headerName: "Descrição", flex: 2 },
    //{ field: "arquivo", headerName: "Arquivo", flex: 2 },
  ];

  return (
    <>
      <Box display="flex" alignItems="center" mb={1}>
        <Typography
          variant="h6"
          color="purple"
          sx={{ cursor: "pointer" }}
          onClick={() => setShowFilters((v) => !v)}
        >
          Filtros de Busca
        </Typography>

        <IconButton
          onClick={() => setShowFilters((v) => !v)}
          size="small"
          sx={{
            transform: showFilters ? "rotate(180deg)" : "rotate(0deg)",
            transition: "0.2s",
            ml: 1,
          }}
        >
          <ExpandMoreIcon />
        </IconButton>
      </Box>

      <Collapse in={showFilters}>
        <Box display="flex" gap={2} mb={2} flexWrap="wrap">
          <TextField
            placeholder="Buscar..."
            size="small"
            value={search}
            onChange={(e) => setSearch(e.target.value)}
            sx={{ width: 260 }}
          />
        </Box>
      </Collapse>

      <div style={{ height: 420, width: "100%" }}>
        <DataGrid rows={filteredRows} columns={columns} />
      </div>
    </>
  );
}
